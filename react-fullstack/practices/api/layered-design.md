---
id: react.api.layered-design
title: Layered API Design
title_zh: 分层 API 设计
domain: api
stage: [api-layer, architecture]
tech_stack: [react, typescript]
applies_when: building an API layer in a React SPA with three or more server resources
applies_when_zh: 在 React SPA 中构建数据获取/API 层，且项目存在 ≥3 个服务端资源
status: stable
related:
  - api.direct-axios-in-component
  - api.dto-as-ui-model
  - api.token-in-api-class
  - api.swallow-error
last_reviewed: 2026-07-07
---

# Layered API Design

## When to apply

Use this when your app fetches data from a server and has **three or more distinct resources** (users, orders, …). Introduce an explicit API layer instead of calling HTTP clients directly from components. Below that threshold (a throwaway demo with 1–2 endpoints), the full layering is overkill — see [Tradeoffs](#tradeoffs).

## Core guidance

Split the API layer into **four layers, each with one reason to change**:

```
Component ──imports──▶ Hook ──imports──▶ API module ──imports──▶ Base client
   UI             React state          single-resource          HTTP transport
                  cache, lifecycle     DTO↔domain mapping        auth, errors, retry
```

**Dependency flows down; data flows up.** Each layer wraps the one below and adds its own concern. Components never know about `axios`; the base client never knows about React.

| Layer | Owns | Typical change trigger |
|-------|------|------------------------|
| Component | UI, interaction | design change |
| Hook (use-case) | cache, loading state, lifecycle | switch to TanStack Query, change retry |
| API module | one resource's shape, DTO↔domain mapping | backend renames a field |
| Base client | HTTP infra: auth, errors, timeout, retry | swap axios → fetch |

### Why four layers (not three)

Merging any two adjacent layers collapses **distinct concerns** into one file:

- **Merge Hook + API module** → data fetching gets welded to React; you can't call it from a script, a worker, or a non-React test. The query function passed to TanStack Query becomes a rewriting task every time.
- **Merge API module + Base client** → swapping the HTTP library touches every resource file; token injection is copy-pasted N times.

Four layers is "just enough" — the minimum where (a) swapping the HTTP library doesn't touch business code, (b) testing data fetching doesn't require rendering a component, and (c) DTOs never leak into component props.

### The data shape morphs at each boundary

A request's payload changes form **three times** as it travels up:

```
HTTP body
  { user_id, profile: { display_name, avatar_url, created_at } }   ← wire format (DTO)
     │
  [Base client]  inject token → request → parse → normalize errors
     │  Promise<UserDTO>
     ▼
  [API module]   toUser(dto)
     │  Promise<User>          ← domain model (app-internal shape)
     ▼
  [Hook]         TanStack Query wrapper: cache / dedup / retry / loading
     │  { data?: User, isLoading, error }
     ▼
  [Component]    reads user.displayName
```

The discipline: **DTOs stop at the API module.** Components only ever see `User`, never `UserDTO`.

### Layer 1 — Base client (singleton, app-wide)

One instance per app. Handles cross-cutting transport concerns.

```typescript
// lib/api/baseClient.ts
import axios, { AxiosError, type AxiosInstance } from 'axios';
import { authStore } from '@/features/auth/authStore';

// Normalize every HTTP failure into one app-level error type.
export class ApiError extends Error {
  constructor(
    public status: number,
    public code: string,
    message: string,
  ) {
    super(message);
    this.name = 'ApiError';
  }
}

const instance: AxiosInstance = axios.create({
  baseURL: import.meta.env.VITE_API_BASE_URL,
  timeout: 10_000,
});

// Auth is INJECTED from an external store — never hardcode tokens here
// (avoids api.token-in-api-class; base client stays reusable across auth schemes).
instance.interceptors.request.use((config) => {
  const token = authStore.getToken();
  if (token) config.headers.Authorization = `Bearer ${token}`;
  return config;
});

// Error normalization: callers above never need to check axios.isAxiosError().
instance.interceptors.response.use(
  (res) => res,
  (error: AxiosError<{ code?: string; message?: string }>) => {
    if (!error.response) throw new ApiError(0, 'NETWORK', 'Network error');
    const { status, data } = error.response;
    throw new ApiError(status, data?.code ?? 'UNKNOWN', data?.message ?? 'Request failed');
  },
);

export const baseClient = {
  get: <T>(url: string) => instance.get<T>(url).then((r) => r.data),
  patch: <T>(url: string, body: unknown) =>
    instance.patch<T>(url, body).then((r) => r.data),
  // post / delete follow the same pattern
};
```

### Layer 2 — API module (one per resource)

DTOs enter and exit here. The boundary functions `toUser` / `toUpdateUserDTO` are the only place wire format is known.

```typescript
// features/users/api/usersApi.ts
import { baseClient } from '@/lib/api/baseClient';

// DTO = wire format (snake_case, ISO strings, nullable fields).
interface UserDTO {
  user_id: string;
  email: string;
  profile: {
    display_name: string;
    avatar_url: string | null;
    created_at: string;
  };
}

// Domain model = app-internal shape (camelCase, Date, defaulted).
export interface User {
  id: string;
  email: string;
  displayName: string;
  avatarUrl: string; // always string — null becomes a default
  createdAt: Date;
}

export interface UpdateUserInput {
  displayName?: string;
  avatarUrl?: string;
}

function toUser(dto: UserDTO): User {
  return {
    id: dto.user_id,
    email: dto.email,
    displayName: dto.profile.display_name,
    avatarUrl: dto.profile.avatar_url ?? '/default-avatar.png',
    createdAt: new Date(dto.profile.created_at),
  };
}

function toUpdateUserDTO(input: UpdateUserInput): {
  display_name?: string;
  avatar_url?: string;
} {
  return {
    display_name: input.displayName,
    avatar_url: input.avatarUrl,
  };
}

export const usersApi = {
  async getById(id: string): Promise<User> {
    const dto = await baseClient.get<UserDTO>(`/users/${id}`);
    return toUser(dto); // DTO is consumed here, never returns above
  },
  async update(id: string, input: UpdateUserInput): Promise<User> {
    const dto = await baseClient.patch<UserDTO>(
      `/users/${id}`,
      toUpdateUserDTO(input),
    );
    return toUser(dto);
  },
};
```

### Layer 3 — Hook (React adapter over the API module)

With TanStack Query, the hook layer is thin — it wraps `usersApi` and adds caching, dedup, retry, and loading flags.

```typescript
// features/users/api/useUser.ts
import { useQuery, useMutation, useQueryClient } from '@tanstack/react-query';
import { usersApi, type User, type UpdateUserInput } from './usersApi';

export function useUserProfile(userId: string) {
  return useQuery<User>({
    queryKey: ['users', userId],
    queryFn: () => usersApi.getById(userId),
    enabled: !!userId,
  });
}

export function useUpdateProfile(userId: string) {
  const qc = useQueryClient();
  return useMutation({
    mutationFn: (input: UpdateUserInput) => usersApi.update(userId, input),
    onSuccess: (updated) => {
      qc.setQueryData(['users', userId], updated);
    },
  });
}
```

### Layer 4 — Component (UI only)

The component knows only `User`. It never imports axios, never sees a DTO, never inspects HTTP status codes. `Skeleton` and `ErrorState` are placeholders for your own UI primitives.

```tsx
// features/users/components/ProfileCard.tsx
import { useUserProfile, useUpdateProfile } from '../api/useUser';

// Replace with your own UI primitives.
function Skeleton() {
  return <div aria-busy="true">Loading…</div>;
}
function ErrorState({ error }: { error: unknown }) {
  return <div role="alert">{String(error)}</div>;
}

export function ProfileCard({ userId }: { userId: string }) {
  const { data: user, isLoading, error } = useUserProfile(userId);
  const updateProfile = useUpdateProfile(userId);

  if (isLoading) return <Skeleton />;
  if (error) return <ErrorState error={error} />;
  if (!user) return null;

  return (
    <figure>
      <img src={user.avatarUrl} alt={user.displayName} />
      <figcaption>
        <h1>{user.displayName}</h1>
        <button
          type="button"
          onClick={() => updateProfile.mutate({ displayName: 'New name' })}
          disabled={updateProfile.isPending}
        >
          Rename
        </button>
      </figcaption>
    </figure>
  );
}
```

## Tradeoffs

- **< 3 resources: skip the base client.** A demo with 1–2 endpoints can call axios directly *inside an API module* — the API module layer still earns its keep (it's where DTO conversion happens), but a shared base client is premature. Promote to four layers the moment a **third** resource appears.
- **Already on TanStack Query: the Hook layer is mostly free.** The query hook *is* the hook layer; you don't write a second wrapper. Don't hand-roll a custom `useApi` abstraction over it.
- **No server cache invalidation needed (rare):** if a resource is truly fire-and-forget, `useEffect` + API module is acceptable — but the API module still does DTO conversion.
- **Server-driven UI:** if the server *is* the source of truth for component shapes (e.g. dynamic forms from a schema), the DTO↔domain mapping may collapse — the domain model *is* the schema. This is the one case where `api.dto-as-ui-model` is acceptable, and it should be flagged explicitly.

## Anti-patterns

- **api.direct-axios-in-component** — calling `axios.get()` / `fetch()` directly inside a component. Couples transport to UI, blocks caching/dedup/retry, and spreads auth handling everywhere.
- **api.dto-as-ui-model** — using the server's wire shape (`user.profile.display_name`) directly as component state/props. A backend rename then forces edits scattered across N components, and components are forced to know about nullability/ISO strings.
- **api.token-in-api-class** — hardcoding auth tokens (or `localStorage.getItem('token')`) inside the base client or API module. Couples infra to one auth scheme and blocks reuse. Inject via an external store instead.
- **api.swallow-error** — `try { ... } catch { /* nothing */ }`. Errors vanish silently, debugging becomes guesswork, and users see blank screens with no telemetry. Either surface via the hook's `error` state or rethrow as `ApiError`.

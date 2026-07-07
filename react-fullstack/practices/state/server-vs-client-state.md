---
id: react.state.server-vs-client-state
title: Server State vs Client State
title_zh: 服务端状态与客户端状态的边界
domain: state
stage: [state-design, architecture]
tech_stack: [react, typescript]
applies_when: deciding where to store a piece of state in a React SPA, especially whether data from the server belongs in a store
applies_when_zh: 在 React SPA 中决定一段状态存哪，尤其是来自服务端的数据是否该进全局 store
status: stable
related:
  - state.server-state-in-redux
  - state.derived-in-state
  - state.props-drilling-too-deep
  - react.api.layered-design
  - decide.state-management
last_reviewed: 2026-07-07
---

# Server State vs Client State

## When to apply

Use this whenever you are about to call `useState`, open a Zustand store, or reach for Redux and the value in question **comes from, or reflects, the server**. The single most common state-management mistake is treating server data as if it were client data — storing a fetched user list in Redux and then hand-writing cache invalidation, retry, and dedup logic that a server-cache library already provides.

## Core guidance

There are **three kinds of state**, each with a different source of truth and a different right tool. Picking the tool before classifying the state is the root cause of `state.server-state-in-redux`.

### Classify the state first

| Kind | Source of truth | Goes stale? | Examples | Right tool |
|------|-----------------|-------------|----------|------------|
| **Server state** | The server database | Yes — others can mutate it | user list, order detail, article body | **TanStack Query / SWR** |
| **URL state** | The URL itself | No (it is the truth) | filter, page number, active tab | **URL search params** |
| **Client state** | The browser only | No (only you can change it) | form input, modal open, dark mode | `useState` / Context / store (see below) |

The deciding question is simple: **"If I refreshed the page, should this value come back from the server, come back from the URL, or be reset?"** Server → server-cache lib; URL → URL; reset → client state.

### Server state — use a dedicated cache library

Server state is, by definition, **a cached copy of remote data**. It will go stale. Managing it with `useState` + `useEffect` means re-implementing, badly, what TanStack Query / SWR ship for free:

| You would hand-write | A cache library gives you |
|----------------------|--------------------------|
| `loading` / `error` flags | built-in `isLoading`, `error` |
| caching across mounts | cache by `queryKey` |
| request deduplication | same key → one request |
| stale-while-revalidate | show stale, refetch in background |
| retry on failure | configurable retry |
| race conditions, cleanup | handled internally |

```typescript
// Server state: the whole pattern is two lines.
import { useQuery } from '@tanstack/react-query';
import { usersApi } from '@/features/users/api/usersApi'; // the API module from react.api.layered-design

export function useUserProfile(userId: string) {
  return useQuery({
    queryKey: ['users', userId],
    queryFn: () => usersApi.getById(userId),
  });
}
```

This is the **hook layer** of `react.api.layered-design`. The two Practices are designed to compose: the API module owns *how* to talk to the server; TanStack Query owns *how* to cache the result.

**Shared cache, single request.** Two components using the same `queryKey` read the same cached object and trigger only one network request — the library deduplicates by key. This is precisely the cross-component sharing that developers wrongly try to achieve by putting server data into Redux.

### URL state — the URL is the source of truth

Anything that should survive a refresh, a copy-paste, or a browser back-button belongs in the URL: filter values, current page, active tab, sort order.

```typescript
import { useSearchParams } from 'react-router-dom';

export function useProductFilters() {
  const [params, setParams] = useSearchParams();
  const page = Number(params.get('page') ?? '1');
  const category = params.get('category') ?? 'all';

  const setCategory = (c: string) => {
    const next = new URLSearchParams(params);
    next.set('category', c);
    next.delete('page'); // reset to first page on new category
    setParams(next);
  };

  return { page, category, setCategory };
}
```

Why prefer URL over client state: it is shareable (send a link), refreshable (F5 keeps the filter), and requires no store at all.

### Client state — pick by sharing pattern and change frequency

Only after ruling out server and URL state do you reach for client-state tools. Pick by **how many components share it** and **how often it changes**:

| Pattern | Tool | Why |
|---------|------|-----|
| One component | `useState` / `useReducer` | no sharing needed |
| A few components, **low-frequency** change (theme, locale) | **Context** | simple, React-native, no extra dep |
| A few / many components, **high-frequency** or complex (cart, multi-step wizard) | **Zustand** (default) / Redux Toolkit (existing Redux codebase) | precise subscriptions avoid the Context re-render trap |

```tsx
// Client state, shared, high-frequency: Zustand.
import { create } from 'zustand';

interface CartState {
  items: string[];
  addItem: (item: string) => void;
}

export const useCartStore = create<CartState>((set) => ({
  items: [],
  addItem: (item) => set((s) => ({ items: [...s.items, item] })),
}));

// Precise subscription: only re-renders when `items` changes.
function CartBadge() {
  const count = useCartStore((s) => s.items.length);
  return <span>{count}</span>;
}
```

Prefer **Zustand** for new code: no Provider boilerplate, ~1KB, accessible outside React (e.g. from the base client in `react.api.layered-design`). Reach for **Redux Toolkit** only when the team already has Redux, or needs time-travel debugging and the middleware ecosystem.

### Derived state — never store it

If a value can be **computed from existing state or props**, do not store it. Compute it during render. Storing derived values creates a second source of truth that must be kept in sync (usually via `useEffect`, which is itself a smell — see `state.derived-in-state`).

```tsx
// Bad: storing what can be computed, then syncing via useEffect.
import { useEffect, useState } from 'react';

function ItemListBad() {
  const [items, setItems] = useState<string[]>([]);
  const [count, setCount] = useState(0);                   // derives from items
  useEffect(() => { setCount(items.length); }, [items]);   // sync tax
  return <ul>{items.map((i) => <li key={i}>{i}</li>)}</ul>;
}
```

```tsx
// Good: compute during render — no second source of truth.
import { useState } from 'react';

function ItemListGood() {
  const [items, setItems] = useState<string[]>([]);
  const count = items.length;                              // no sync, no drift
  return <ul>{items.map((i) => <li key={i}>{i}</li>)}</ul>;
}
```

For expensive derivations, `useMemo` — not state.

## Tradeoffs

- **Tiny demo (1–2 components, no server data):** skip the classification entirely; `useState` everywhere is fine. The cost of the model exceeds its benefit until the app grows a second shared value.
- **Existing Redux codebase:** you do not have to rip it out. Keep client state in Redux; just **stop putting server cache in it**. New server fetching should use TanStack Query alongside Redux — they coexist cleanly (TanStack Query for server cache, Redux for client state).
- **Real-time / websocket data:** still server state. Libraries like TanStack Query integrate with websockets via query invalidation; the classification does not change just because the transport is push.
- **Forms:** form field values are client state while editing, but once submitted they become server state (the server is the new source of truth). Libraries like React Hook Form manage the client phase; on submit you hand off to the server-cache layer.

## Anti-patterns

- **state.server-state-in-redux** — storing server-fetched data in Redux/Zustand and hand-managing cache invalidation, retry, and dedup. Reimplements a server-cache library poorly; the data still goes stale with no mechanism to detect it.
- **state.derived-in-state** — storing a value that can be computed from existing state/props (e.g. `count` derived from `items.length`), then syncing it with `useEffect`. Creates a second source of truth and an extra render cycle.
- **state.props-drilling-too-deep** — passing a value down through more than two component layers that do not use it, instead of lifting to a store/Context or restructuring via composition.

## Related decisions

The tool selection in this Practice is encoded as a decision graph in `decisions.yaml` — see `decide.state-management`. `lore decide` walks that tree from project context (state origin + sharing pattern) to a recommendation.

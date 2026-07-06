# Lorelum 前端知识包设计提案：`react-fullstack`

> **状态：草案 v0.1 · 仅供讨论**
> 目标读者：Lorelum 维护者 + 前端 contributors
> 关联：引擎与格式规范尚在 `lorelum/lorelum` 中定义（见其 README/CONTRIBUTING）。本提案同时作为对 **Practice/pack 格式**的真实内容验证。

---

## 1. 这份文档要回答的问题

在写任何一条 Practice 之前，先把五件事钉死，否则会批量返工：

1. 这个包**覆盖什么、不覆盖什么**？
2. 知识包的**目录怎么组织**？
3. **Practice 的格式**长什么样（frontmatter 字段、正文结构、反模式条目）？
4. 怎么给 Practice **分类与编号**（domain / id 约定）？
5. **先写哪些**，路线怎么排？

后续所有 Practice 内容都按这份契约来产出。本文档**不**包含完整 Practice 正文——那是定稿后的批量工作。

---

## 2. 背景与定位

Lorelum 的核心是"按需检索、精准注入"。一个 Practice 只有在**当下有用**时被检索出来才有价值。这对前端知识包的设计意味着：

- **粒度要细、触发条件要明确**：`applies_when` 是 Practice 能否被正确检索的命脉，写糊了等于这条 Practice 不存在。
- **要承载决策，不只是规则**：前端选型（状态管理、样式方案、表单库）没有标准答案，必须靠 `decisions.yaml` 把"在什么上下文下选什么"沉淀下来——这正是 `.cursorrules` 做不到、Lorelum 的差异化价值所在。
- **反模式比正面规则更好用**：AI 写出反模式代码的频率远高于"忘记正面规则"，`lore check` 这条产品线要求反模式必须有可机器识别的 id。

`react-fullstack` 在路线图里是 P3–P4 的**第一个公开包**，它的质量直接定义了"一个优秀的 Lorelum 知识包长什么样"。我们是在为整个生态打样。

---

## 3. 设计原则

| 原则 | 含义 | 反例 |
|------|------|------|
| **Need-to-know** | 一条 Practice 只讲一件事，触发条件精确 | 把"React 项目所有规范"塞进一条 |
| **可检索优先** | frontmatter 字段为检索服务，正文为理解服务 | 把关键信息只写在正文 prose 里 |
| **带主张** | 给推荐，给理由，给反例；不做中立百科 | "状态管理有很多选择，看情况" |
| **可演进** | 字段支持 `status` / `last_reviewed`，允许过时 | 写死、无版本、无法废弃 |
| **内容自包含** | 一条 Practice 不依赖另一条的正文才能理解 | "如前所述"式串联 |
| **反模式一等公民** | 每个反模式有稳定 id，能被 `lore check` 引用 | 散落在 prose 里的口头警告 |

---

## 4. 范围：React 全家桶

### 4.1 In scope（覆盖）

- **React 18+**（hooks 优先，concurrent rendering）
- **TypeScript**（默认强类型，不写纯 JS 实践）
- **客户端路由**（React Router / TanStack Router 为主，兼顾理念）
- **状态管理**：客户端状态（Context / Zustand / Redux Toolkit）+ 服务端状态（TanStack Query / SWR）的**选型与边界**
- **API 层**（HTTP client 抽象、DTO 边界、错误处理、请求生命周期）
- **组件设计**（分层、组合、props 设计、受控/非受控）
- **表单**（受控、校验、提交、表单库选型）
- **样式**（方案选型、设计 token、主题——给理念，不绑死单一方案）
- **性能**（渲染、bundle、代码分割、列表/资源优化）
- **测试**（组件测试、E2E、MSW mock）
- **错误处理**（Error Boundary、全局错误、上报）
- **可访问性 a11y**（作为横切，融入相关 Practice）

### 4.2 Out of scope（不覆盖，留给别的包或后续）

- **SSR / RSC / Next.js / Remix 等元框架** → 未来独立包 `react-metaframeworks`（渲染模型差异大，混在一起会稀释触发精度）
- **移动端 React Native** → 独立包
- **构建工具链深水区**（Vite/Webpack 配置、Babel 插件）→ 通用 `tooling` 层只放少量实践
- **CI/CD、部署、监控** → 非前端专属，留给通用包
- **微前端** → 独立专题包

> 🟡 **讨论点 A**：Next.js / RSC 是否真的先排除？社区主流是 Next，把它全排除可能让首包"看起来不接地气"。一种折中：核心包纯客户端，单独有 `react.rsc.*` 少量标记 `status: provisional` 的 Practice 占位。**我的倾向：先排除，保持触发精度，但留一个明确的占位领域。**

### 4.3 目标用户画像

- **团队**：用 React + TS 做 SPA、需要把团队规范固化下来的中小团队（Lorelum 的核心付费意愿来源）。
- **个人**：用 Cursor / Claude Code 的独立开发者，想拿到"大厂级"前端默认值。
- **不针对**：纯新手学 React（这不是教程仓库）；用 Vue/Svelte 的（留给别的包）。

---

## 5. 知识包目录结构（草案）

```
react-fullstack/
├── pack.yaml                  # 知识包清单（id / 版本 / tech_stack / 包含的领域）
├── decisions.yaml             # 决策图谱（状态/样式/表单等选型树）
├── practices/
│   ├── architecture/
│   │   ├── feature-based-structure.md
│   │   └── module-boundaries.md
│   ├── api/
│   │   ├── layered-design.md
│   │   ├── error-handling.md
│   │   └── request-lifecycle.md
│   ├── state/
│   │   ├── client-vs-server-state.md
│   │   └── url-as-state.md
│   ├── routing/
│   │   ├── permission-guard.md
│   │   └── code-splitting.md
│   ├── components/
│   ├── forms/
│   ├── styling/
│   ├── performance/
│   ├── testing/
│   └── errors/
├── anti-patterns/
│   └── index.yaml             # 反模式集中登记（id / 描述 / 关联 Practice / 检测线索）
└── templates/
    ├── feature-module/        # 可脚手架的模板（带文件结构）
    └── api-module/
```

**几个关键决策：**

- **Practice 按 domain 分目录**，文件名 kebab-case，一条 Practice 一个文件。便于检索引擎按路径过滤，也便于人浏览。
- **反模式集中登记在 `anti-patterns/index.yaml`**，而不是分散在各 Practice。理由：同一个反模式可能被多条 Practice 引用；`lore check` 需要一个稳定、可枚举的反模式表。Practice 正文里只引用反模式 id。
- **模板放 `templates/`**，是可被 `lore` 脚手架引用的代码骨架（区别于 Practice 的"指导文字"）。
- **`pack.yaml` 是清单**，声明这个包的元信息与所含领域，供 `lore install` / `lore search` 使用。

> 🟡 **讨论点 B**：反模式是集中放还是随 Practice 放？集中放便于 `lore check`，但作者改一条 Practice 时要跳两个地方。**我的倾向：登记集中（`index.yaml` 为准、有 id/检测线索），详细解释随对应 Practice 正文。** 也就是"索引集中、叙事分散"。

---

## 6. Practice 格式规范（草案）

> 本节是对 `lorelum/lorelum` README 中 Practice 范例的**扩展提案**。README 已确立的字段（`id` / `stage` / `tech_stack` / `applies_when`）保持兼容，不擅自改动——只在其上做加法。

### 6.1 Frontmatter 字段

| 字段 | 必填 | 类型 | 说明 |
|------|:---:|------|------|
| `id` | ✅ | string | 全局唯一，点分命名空间（见 §8） |
| `title` | ✅ | string | 英文标题（`# 标题`的镜像，便于检索结果展示） |
| `title_zh` | ✅ | string | 中文标题。检索关键字段双语，见 §6.5 语言策略 |
| `stage` | ✅ | string[] (≤3) | 开发阶段/触发阶段数组，**单条最多 3 个**，见下方枚举与约束 |
| `tech_stack` | ✅ | string[] | 关联技术，如 `[react, typescript]` |
| `applies_when` | ✅ | string | 英文**触发条件**（自然语言，检索命中的关键） |
| `applies_when_zh` | ✅ | string | 中文触发条件。检索关键字段双语，见 §6.5 语言策略 |
| `domain` | ✅ | string | 所属领域（§7 表中的 key） |
| `status` | ➖ | enum | `draft` \| `stable` \| `provisional` \| `deprecated`，默认 `stable` |
| `related` | ➖ | string[] | 关联 Practice id 或反模式 id |
| `tags` | ➖ | string[] | 辅助检索的自由标签 |
| `last_reviewed` | ➖ | date | `YYYY-MM-DD`，最后人工复核日期 |

**`stage` 建议枚举**（对齐 AI 协作的真实阶段，便于按阶段检索）：

`project-setup` · `architecture` · `feature-implementation` · `api-layer` · `state-design` · `ui-build` · `form` · `routing` · `testing` · `refactor` · `review`

> ✅ **已决（issue #1）**：`stage` 为**多值数组**，单条最多 3 个，且必须是最强相关的阶段。引擎按集合匹配召回（用户当前阶段 ∈ Practice.stage）。上限 3 由校验脚本强制，防止"全标上"导致字段退化。此结论需回流到 `lorelum/lorelum` 的检索模型 spec。

> ✅ **已决（issue #2）**：保持 `applies_when`，不改名。理由：主仓库 README 已将其作为公共 Practice 范例的字段名，改名属破坏性变更；且 `applies_when`（"在什么情况下适用"）语义比 `trigger` 更适合写自然语言触发条件。若未来主仓库 spec 决定改名，本仓库届时跟随。

> ✅ **已决（issue #4）**：知识包采用**英文为主 + 检索字段双语**策略。`title`/`applies_when` 英文必填，`title_zh`/`applies_when_zh` 中文必填（平铺后缀，非结构化对象）。详见 §6.5 语言策略。

### 6.2 正文结构

```markdown
# <标题>

## 何时适用
<1–3 句把 applies_when 展开，给 AI 明确的"是我/不是我"判断>

## 核心指引
<分小节给出具体怎么做。代码示例必备。>

## 权衡
<什么情况下不这么做，替代方案>

## 反模式
- <anti-pattern-id>：<一句话>
```

约束：
- **代码示例用 TS + 函数组件 + hooks**（与 §4 默认一致）。
- **每个核心论断尽量配代码**，AI 仿写代码比仿写 prose 准。
- **正文不重复 frontmatter 已有的信息**。

### 6.3 反模式条目（登记在 `anti-patterns/index.yaml`）

```yaml
- id: api.direct-axios-in-component
  domain: api
  summary: 在 React 组件里直接调用 axios / fetch
  why_bad: |
    把数据获取与 UI 耦合，无法复用、难以测试、无法统一处理鉴权/错误/重试。
  relates_to: [react.api.layered-design]
  severity: major
  detection:                       # 可选。弱线索，非可靠检测方案。
    - regex: "axios\\.(get|post|put|delete)\\("
                                   # 引擎可消费作初筛，也可忽略；最终判断由引擎的
                                   # AST/类型分析能力完成。pack 作者不背"写可靠检测器"的负担。
```

**字段定位：**
- `summary` / `why_bad` / `relates_to` / `severity` —— **必填**，人类可读，描述"是什么、为什么坏"。
- `detection` —— **可选**，给引擎的弱线索（正则/启发式）。pack 作者写不出可靠检测器时，留空即可。

> ✅ **已决（issue #3）**：检测由**引擎承担**，pack 只提供 `summary` / `why_bad` / `relates_to` / `severity`（必填）+ 可选的 `detection` 弱线索。
>
> **技术根据：** 正则检测"看脸"（误报漏报都高），AST 检测"看骨"（可靠但要解析器+遍历器，门槛高）。反模式的本质多为结构性问题（"调用出现在错误上下文""依赖不匹配""状态可派生却存储"），必须靠 AST 才能可靠识别。让 pack 作者（前端专家）写 AST 检测器是能力错配。故：可靠检测归 `lore check` 引擎（专业工具链），pack 只给人类可读描述 + 可选的字面弱线索（引擎可消费作初筛、也可忽略）。

### 6.4 完整 Practice 范例（基于 README，补全字段）

见 §11 末尾的 `react.api.layered-design` 范例。

### 6.5 语言策略（issue #4）

知识包采用**英文为主 + 检索字段双语**。规则：

| 内容 | 语言 | 说明 |
|------|------|------|
| 正文 prose（核心指引、权衡、反模式叙事） | **英文为主** | 关键术语可在括号注中文，如 "DTO boundary（数据传输对象边界）" |
| 代码示例 + 代码注释 | **全英文** | 与开源惯例一致 |
| `title` / `applies_when` | **英文**（必填） | 检索关键字段，主版本 |
| `title_zh` / `applies_when_zh` | **中文**（必填） | 平铺后缀字段，让中文 query 也能命中关键字段 |
| 反模式 `summary` / `why_bad` | **英文为主** | 反模式 id 全局复用，英文降低跨语言歧义 |
| `decisions.yaml` 的 `question` / `ask` | 英文，可补中文 | 决策树节点的提问文本 |

**为什么用平铺后缀（`title` + `title_zh`）而非结构化对象（`title: { en, zh }`）：**
- 对引擎解析逻辑改动最小（YAML 标量字段，无需支持对象类型）；
- 对作者直观（写两行而非嵌套）；
- 本仓库是内容仓库，不该推动 spec 复杂化。

**为什么正文不全双语：**
- 维护成本翻倍，且 CC-BY-4.0 内容面向全球社区；
- 正文是给人/AI **理解**用的，英文为主 + 术语括注中文已可读；
- 检索**命中**靠关键字段（title/applies_when），这两类双语即可保证中文 query 不漏召回。

---

## 7. 领域划分（domain 体系）

| domain | 职责 | 示例 Practice | 示例 stage |
|---|---|---|---|
| `architecture` | 项目结构、模块边界、分层 | feature-based 结构、模块依赖方向 | architecture |
| `api` | HTTP 抽象、DTO、错误、生命周期 | 分层 API、错误处理、请求竞态 | api-layer |
| `state` | 客户端/服务端状态、URL 状态 | 客户端 vs 服务端状态边界 | state-design |
| `routing` | 路由组织、权限、分割 | 权限路由、懒加载 | routing |
| `components` | 组件分层、props、组合 | 展示/容器分离、受控边界 | ui-build |
| `forms` | 受控、校验、提交、选型 | 表单状态、校验时机 | form |
| `styling` | 方案选型、token、主题 | 样式分层、设计 token | ui-build |
| `performance` | 渲染、bundle、分割、列表 | memo 边界、虚拟列表 | refactor |
| `testing` | 组件、E2E、mock | 组件测试边界、MSW | testing |
| `errors` | Error Boundary、上报、降级 | 错误边界、用户态错误上报 | feature-implementation |

原则：**domain 是稳定骨架，Practice 是可增删的肉**。新增领域需要讨论（影响 id 命名空间），新增 Practice 不需要。

> 🟡 **讨论点 F**：`a11y` 和 `typescript` 没有单列 domain。我的考虑：a11y 是横切（融入 components/forms/performance），typescript 是默认底座（不单列，但有类型相关的强实践挂在对应 domain 下，如 `api.dto-typing`）。**是否要单列 `typescript` domain？倾向不单列。**

---

## 8. id 命名约定

格式：`<stack>.<domain>.<topic>`

- `stack` 固定为 `react`（本包内）。多栈并存时由 `pack.yaml` 的命名空间隔离，不把栈写死进 id 也行——**待和引擎对齐**。
- `domain` 取 §7 表的 key。
- `topic` 为 kebab-case 短描述，如 `layered-design`、`server-vs-client-state`。

反模式 id 用**两级**：`<domain>.<short-description>`（不带 stack 前缀，因为反模式往往跨栈复用，如 `state.server-state-in-redux` 在 React/Vue 都成立）。

```
Practice:   react.api.layered-design
            react.state.server-vs-client-state
            react.routing.permission-guard
反模式:     api.direct-axios-in-component
            state.server-state-in-redux
            effect.unconditional-fetch
```

> 🟡 **讨论点 G**：反模式 id 是否需要栈前缀？`api.direct-axios-in-component` 明显是前端/React 语境，但 `state.spread-props-everywhere` 就跨栈。**倾向：不带栈前缀，靠 domain 区分；若反模式确实栈特定，再升格命名。**

---

## 9. 决策图谱 `decisions.yaml`（草案）

这是 Lorelum 区别于 `.cursorrules` 的**王牌能力**。前端最大的痛点不是"不知道规则"，而是"不知道该选哪个"。`lore decide` 根据项目上下文走决策树给出推荐。

**范例：状态管理选型**（节选）

```yaml
- id: decide.state-management
  question: 这个状态应该放哪？
  inputs:
    - key: sharing
      ask: 这个状态被几个组件共享？
      options: [single, few-cross-tree, app-wide, none-persistent]
    - key: origin
      ask: 状态来源？
      options: [server-cache, user-input, ui-transient, url]
  rules:
    - if: { origin: server-cache }
      then: { recommend: TanStack Query / SWR, practice: react.state.server-vs-client-state }
    - if: { origin: url }
      then: { recommend: URL search params, practice: react.state.url-as-state }
    - if: { sharing: single }
      then: { recommend: useState / useReducer }
    - if: { sharing: app-wide }
      then: { recommend: Zustand 或 Redux Toolkit, practice: react.state.client-store }
      note: 中等复杂度优先 Zustand；已有 Redux 生态或 time-travel 需求用 RTK
    - if: { sharing: few-cross-tree }
      then: { recommend: Context（仅低频变更）或 Zustand }
  anti_patterns_to_check:
    - state.server-state-in-redux
```

`decisions.yaml` 的格式最终由引擎（P5 决策图谱执行器）定义。**这里只是表达"前端知识包需要 decisions.yaml 长这样"的内容诉求**——具体 DSL 待和引擎方对齐。

初始决策图谱覆盖：**状态管理 · 样式方案 · 表单方案 · 路由方案 · 数据获取策略**。

> 🟡 **讨论点 H**：`lore decide` 的输入是自然语言（"React SPA, medium client state, ..."）还是结构化字段？两种都要支持的话，`decisions.yaml` 需要同时声明 `inputs`（结构化）和语义检索的桥接。**这是产品级问题，需在 `lorelum/lorelum` 那边定，本包先按结构化 inputs 写。**

---

## 10. 模板 `templates/`

可被 `lore` 脚手架直接落地的代码骨架，与 Practice 的"指导文字"互补。初始：

- `feature-module/`——一个 feature 的标准目录（api/state/components/tests 子目录 + index）
- `api-module/`——一个 API 模块（基于 base client 的单资源 CRUD）
- `component/`——展示组件 / 容器组件骨架
- `form/`——受控表单 + 校验骨架

模板默认 **TS + 函数组件 + hooks**，不绑死具体库（库选型由对应 Practice + decisions.yaml 引导）。

---

## 11. 反模式清单（初始集，按 domain）

> 命名见 §8。每条会在 `anti-patterns/index.yaml` 完整登记（§6.3）。

**api**
- `api.direct-axios-in-component` — 组件内直接调 http client
- `api.dto-as-ui-model` — DTO 直接当组件 state
- `api.token-in-api-class` — 鉴权态写死在 API 类内部
- `api.swallow-error` — catch 后不处理（吞错误）

**state**
- `state.server-state-in-redux` — 服务端缓存塞进全局 store 手动维护
- `state.derived-in-state` — 可计算得出的值存进 state
- `state.props-drilling-too-deep` — props 透传超过 2 层未抽状态/组合

**effect / hooks**
- `effect.unconditional-fetch` — useEffect 无条件 fetch 且无清理
- `effect.stale-closure-deps` — 依赖数组缺失/错误
- `effect.sync-derived-state` — 用 effect 同步可计算的状态（`setState(prev => ...)` 的滥用）

**components**
- `component.logic-in-presentational` — 业务逻辑写在纯展示组件里
- `component.giant-component` — 单组件超过 ~200 行未拆分
- `component.spread-props-blindly` — `{...props}` 无类型约束透传

**routing**
- `routing.client-only-auth` — 权限只在客户端路由做、无后端兜底
- `routing.eager-everything` — 不做代码分割的全量 bundle

**testing**
- `testing.implementation-detail` — 测实现细节而非行为
- `testing.real-network` — 单测打真实网络

**styling**
- `styling.magic-values` — 散落的硬编码颜色/间距，未走 token

**types**
- `types.any-everywhere` — `any` 满天飞
- `types.non-null-assertion-abuse` — 滥用 `!`

---

### 完整 Practice 范例（基于 README 补全字段）

```markdown
---
id: react.api.layered-design
title: Layered API Design
title_zh: 分层 API 设计
domain: api
stage: [api-layer, architecture]
tech_stack: [react, typescript]
applies_when: building an API layer in a React SPA
applies_when_zh: 在 React SPA 中构建数据获取/API 层
status: stable
related:
  - api.direct-axios-in-component
  - api.dto-as-ui-model
  - react.state.server-vs-client-state
last_reviewed: 2026-07-06
---

# Layered API Design

## 何时适用
当你的组件需要从服务端获取数据、且项目存在 ≥3 个数据资源时，应该建立分层的 API 抽象，而不是在组件里直接发请求。

## 核心指引
分四层，单向依赖：组件 → hooks/use-case → API module → base client。
（此处配 TS 代码示例：base client（拦截器/鉴权/错误）→ 单资源 module → 调用方 hook）

## 权衡
- 小 demo（1–2 个请求）可以暂不抽 base client，但 module 层从第一天就该有。
- 数据获取若已用 TanStack Query，hooks 层由 query hook 承担，不必再造。

## 反模式
- api.direct-axios-in-component：组件内直接调 http client
- api.dto-as-ui-model：DTO 直接当组件 state（应在校验/转换层转 UI 模型）
- api.token-in-api-class：鉴权态写死在 API 类内部
```

---

## 12. 产出路线

按"对检索价值最大、对格式验证最有代表性"排序：

| 阶段 | 产出 | 目的 |
|------|------|------|
| **M0** | 本设计文档定稿 | 钉契约 |
| **M1** | `react.api.layered-design` + `react.state.server-vs-client-state` 两条深度样例 + 反模式登记 + `decisions.yaml` 状态选型 | 用真实内容**验证格式**，反推引擎需求 |
| **M2** | architecture / routing / components 三领域各 2–3 条 | 验证 domain 划分与 id 体系 |
| **M3** | forms / styling / testing 补齐 | 形成可用广度 |
| **M4** | performance / errors + 全量反模式复核 + templates | 接近首包发布质量 |

M1 是关键——**先把两条 Practice 打磨到能当范例的程度，再扩**。不要 20 条半成品。

---

## 13. 开放问题（需讨论后定稿）

| # | 问题 | 我的倾向 |
|---|------|---------|
| A | Next.js / RSC 是否纳入首包 | 先排除，留占位领域 |
| B | 反模式集中登记 vs 随 Practice | 索引集中、叙事分散 |
| ~~C~~ | ~~`stage` 单值还是多值~~ | ✅ **已决（#1）**：多值数组，单条 ≤3 个，集合匹配召回 |
| ~~D~~ | ~~`applies_when` 是否改名 `trigger`~~ | ✅ **已决（#2）**：保持 `applies_when`，破坏性改名无足够收益 |
| ~~E~~ | ~~反模式检测能力由 pack 还是引擎承担~~ | ✅ **已决（#3）**：引擎承担（AST）；pack 必填 summary/why_bad/relates_to/severity，detection 可选作弱线索 |
| F | 是否单列 `typescript` / `a11y` domain | 不单列 |
| G | 反模式 id 是否带栈前缀 | 不带，靠 domain 区分 |
| H | `lore decide` 输入：自然语言还是结构化 | 待引擎定；pack 先按结构化写 |
| I | `pack.yaml` 的确切 schema | 本提案只给轮廓，需与引擎对齐 |
| ~~J~~ | ~~多语言（本包用中文还是中英双语）~~ | ✅ **已决（#4）**：英文为主 + 检索字段双语（title/applies_when 平铺后缀 _zh）；详见 §6.5 |

> 🟡 **讨论点 J（语言）**：主仓库 README 是中英双语，CONTRIBUTING/AGENTS 是英文。知识包内容面向全球社区（CC-BY-4.0），**英文是默认**；但维护者显然重视中文受众。**我的倾向：Practice 正文以英文为主、关键术语配中文注释；`applies_when` / `title` 这类检索字段中英都给（用 `title` + `title_zh` 之类），让检索对中文 query 也友好。** 这个会影响 frontmatter schema，需要早定。

---

## 附：与 `lorelum/lorelum` 的协作边界

本提案**不定义** Practice/pack 的最终格式规范——那是引擎仓库的公共契约（CONTRIBUTING 明确：格式变更需先 design 讨论）。本提案的角色是：

1. **作为内容方**，提出"前端知识包需要格式支持 X/Y/Z"的诉求（见开放问题 C/D/E/H/I/J）；
2. **作为格式的试金石**，用 M1 的两条深度 Practice 反向验证格式是否够用；
3. 任何**格式层面的决定**回流到 `lorelum/lorelum` 的 spec issue 里推动，不在此仓库私自定义。

---

*本提案欢迎在 Discussions 或本仓库 issue 中逐条评议。请优先对 §13 的开放问题给出判断。*

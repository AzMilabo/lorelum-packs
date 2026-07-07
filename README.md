<p align="center">
  <h1 align="center">Lorelum Packs</h1>
  <p align="center">Lorelum 的社区知识包仓库：把团队工程经验切成 Practice。</p>
  <p align="center">
    <a href="./LICENSE"><img alt="License" src="https://img.shields.io/badge/license-CC--BY--4.0-blue"></a>
    <a href="https://github.com/lorelum/lorelum"><img alt="Status" src="https://img.shields.io/badge/status-early%20development-orange"></a>
    <a href="./DESIGN.md"><img alt="Design" src="https://img.shields.io/badge/design-draft%20v0.1-lightgrey"></a>
  </p>
  <p align="center">
    <a href="https://github.com/lorelum/lorelum">主仓库 lorelum/lorelum</a>
  </p>
</p>

---

> ⚠️ **早期开发中。** 知识包内容与 Practice/pack 格式规范均在设计中，尚不可用。当前进度见 [DESIGN.md](./DESIGN.md)。

## 这个仓库是什么

[**Lorelum**](https://github.com/lorelum/lorelum) 把团队工程经验切成**离散、可检索、带触发条件的 Practice**，在 AI 编码工具（Cursor / Claude Code / Codex / Windsurf）需要的时候精准注入，而不是一开始全量灌进上下文。

**本仓库存放"被注入的内容"——知识包（Knowledge Packs）**。一个知识包把多条 Practice + 决策图谱（`decisions.yaml`）+ 模板 + 反模式打包，绑定到一个技术栈或团队标准。

引擎（CLI、检索、MCP、格式规范）在主仓库 [`lorelum/lorelum`](https://github.com/lorelum/lorelum)（Apache 2.0）。本仓库**只**包含知识包内容（CC-BY-4.0）。

```
lorelum/lorelum        ← 引擎与格式规范（Apache 2.0）
lorelum/lorelum-packs  ← 知识包内容（CC-BY-4.0）  你在这里
```

## 当前进展

| 阶段 | 内容 | 状态 |
|------|------|------|
| M0 | 知识包设计提案 | 📄 [DESIGN.md](./DESIGN.md)（草案，待评议） |
| M1 | 首批深度样例 Practice（验证格式） | 待启动 |
| M2+ | 各领域 Practice 扩充 | 规划中 |

**第一个公开包**计划为 `react-fullstack`（对齐主仓库路线图的 P3–P4）。设计范围、领域划分、Practice 格式与开放问题见 [DESIGN.md](./DESIGN.md)。

## 仓库结构

```
.
├── README.md          
├── DESIGN.md          # react-fullstack 知识包设计提案（草案 v0.1）
└── react-fullstack/      # 首个知识包（按 DESIGN.md 落地，M1 起填充）
    ├── pack.yaml         # 知识包清单（待定稿）
    ├── decisions.yaml    # 决策图谱（状态/样式/表单等选型）
    ├── practices/        # 按 domain 分目录的 Practice
    │   ├── architecture/ # 项目结构、模块边界、分层
    │   ├── api/          # HTTP 抽象、DTO、错误处理、生命周期
    │   ├── state/        # 客户端/服务端状态、URL 状态
    │   ├── routing/      # 路由组织、懒加载、守卫接线
    │   ├── auth/         # 鉴权与会话：token 存储/刷新、权限模型、守卫边界
    │   ├── components/   # 组件分层、props 设计、组合
    │   ├── forms/        # 受控、校验、提交、表单库选型
    │   ├── styling/      # 样式方案选型、设计 token、主题
    │   ├── performance/  # 渲染优化、bundle、代码分割、列表
    │   ├── testing/      # 组件测试、E2E、MSW mock
    │   └── errors/       # Error Boundary、全局错误、上报
    ├── anti-patterns/    # 反模式集中登记（index.yaml）
    └── templates/        # 可脚手架的代码模板
```

## 参与贡献

知识包贡献是 Lorelum 的**一等贡献**——Lorelum 的价值就在于其知识包。

- 📖 先读 **[DESIGN.md](./DESIGN.md)**：了解范围、格式约定与开放问题。
- 🤖 用 AI 协作？同时读一下主仓库的 [AGENTS.md](https://github.com/lorelum/lorelum/blob/main/AGENTS.md)。
- 💬 想法或建议，到主仓库 [Discussions](https://github.com/lorelum/lorelum/discussions) 聊聊。
- 🐛 发现内容错误或反模式遗漏？开个 issue。

> 关于开发流程、提交规范、CLA 等，遵循主仓库的 [CONTRIBUTING.md](https://github.com/lorelum/lorelum/blob/main/CONTRIBUTING.md)。本仓库的特有约定会在内容落地后补充。

## License

本仓库的知识包内容采用 **[CC-BY-4.0](./LICENSE)**（国际知识共享 署名 4.0）。

这与主仓库的分层 License 是一致的——能让开发者离线跑通完整流程的部分永远开源。详见主仓库 [README](https://github.com/lorelum/lorelum#license) 的 License 架构说明。

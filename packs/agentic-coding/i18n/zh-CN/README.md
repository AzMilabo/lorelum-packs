# `agentic-coding` 简体中文本地化

本目录提供 `agentic-coding` Pack 的简体中文阅读版本。中文内容用于理解与讨论，不参与安装、检索或运行时注入；[`../../practices`](../../practices/) 中的英文 canonical Practice 是 ID、元数据、反模式 ID 和运行时行为的唯一真源。如中英文存在冲突，以英文 canonical 文件为准。

中文文件与 canonical Practice 保持相同的相对路径，不包含 runtime frontmatter。同步状态由 Lorelum 根据格式化后的英文 Markdown 自动维护，不应手工计算或修改 digest。

## 导航

### 需求

- [定义验收标准与明确的非目标](practices/requirements/define-acceptance-and-non-goals.md)
- [让工作立足于用户目标](practices/requirements/ground-user-goal.md)
- [解决冲突来源之间的权威归属](practices/requirements/resolve-source-authority.md)

### 规划

- [只纳入当前有依据的工作](practices/planning/admit-only-currently-justified-work.md)
- [定义停止与重新规划条件](practices/planning/define-stop-condition.md)
- [将计划映射到用户能力](practices/planning/map-plan-to-user-capability.md)
- [规划最低充分证据](practices/planning/plan-sufficient-evidence.md)
- [按风险与成本调整工作投入](practices/planning/scale-work-to-risk-and-cost.md)

### 实现

- [选择足以满足需求的最小设计](practices/implementation/choose-smallest-sufficient-design.md)
- [确认已授权产品表面的具体变体](practices/implementation/confirm-product-surface-expansion.md)
- [构建前先复用现有能力](practices/implementation/inspect-and-reuse-existing-capability.md)
- [将行为放在不变量的所有者中](practices/implementation/preserve-responsibility-boundaries.md)
- [实现发生重大偏移时重新规划](practices/implementation/replan-on-material-drift.md)
- [显式记录可安全采用的未确认假设](practices/implementation/surface-unconfirmed-assumptions.md)

### 测试

- [将每项测试锚定到契约](practices/testing/anchor-tests-to-requirements.md)
- [断言可观察或稳定的行为](practices/testing/assert-observable-behavior.md)
- [修改测试前先对失败分类](practices/testing/classify-failure-before-changing-test.md)
- [要求回归保护具备证据依据](practices/testing/justify-regression-protection.md)

### 验证

- [将证据绑定到产物状态](practices/verification/bind-evidence-to-artifact-state.md)
- [补齐或声明证据缺口](practices/verification/close-or-declare-evidence-gaps.md)
- [将证据映射到验收标准](practices/verification/map-evidence-to-acceptance.md)

### 审查

- [提交前执行减法审查](practices/review/run-subtractive-review-before-commit.md)
- [采取行动前先验证发现](practices/review/validate-findings-before-action.md)

### 交付

- [只声明证据支持的结果](practices/delivery/claim-only-supported-outcome.md)
- [只报告实质性遗留项](practices/delivery/report-material-residuals.md)

### 纠正

- [恢复权威基线](practices/correction/restore-authoritative-baseline.md)

### 上下文与恢复

- [上下文丢失后重新立足事实](practices/context/reground-after-context-loss.md)
- [继续工作前先验证交接](practices/context/validate-handoff-before-continuation.md)
- [编写决策密集的 Checkpoint](practices/context/write-decision-dense-checkpoint.md)

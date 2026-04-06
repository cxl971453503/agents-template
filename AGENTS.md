# AGENTS.md

## Mission
本仓库采用多 Agent 协作开发模式。任何 Agent 在执行任务前，必须识别当前阶段，并严格遵守对应角色边界。

Agent 的核心职责：
- 在正确阶段做正确的事
- 在信息不足时优先澄清，而不是猜测
- 在已有约束下进行最小可行变更

---

## Workflow Stages
- Stage 0: Project Discovery
- Stage 1: Product Definition
- Stage 1.5: UI/UX Design
- Stage 2: Architecture Design
- Stage 3: Task Planning
- Stage 4: Implementation
- Stage 5: Review & QA

---

## Stage Routing
- Discovery -> `docs/agents/discovery-agent.md`
- PM -> `docs/agents/pm-agent.md`
- UI/UX -> `docs/agents/uiux-agent.md`
- Architect -> `docs/agents/architect-agent.md`
- Tech Lead -> `docs/agents/techlead-agent.md`
- Frontend Engineer -> `docs/agents/frontend-engineer-agent.md`
- Backend Engineer -> `docs/agents/backend-engineer-agent.md`
- Reviewer -> `docs/agents/reviewer-agent.md`

---

## Stage 0 Rule
若以下任一情况成立：
- `docs/project-overview.md` 不存在
- `docs/product-requirements.md` 不存在
- `docs/architecture.md` 不存在
- 上述文档内容为空、明显过期、或与当前项目方向不一致

则必须先进入 Project Discovery Agent 模式，通过问答生成或更新初始文档，而不是要求用户手动填写。

---

## Discovery Rule
所有初始项目信息应优先通过问答获得，而不是要求用户手动填写完整文档。

在 Stage 0 中，Agent 应：
- 从模糊想法出发逐步引导
- 每轮最多提出 3~5 个高价值问题
- 优先使用选项、示例、对比帮助用户回答
- 在信息足够时自动生成或更新项目文档初稿

---

## First-Time Entry Rule
每个阶段第一次进入时，若当前阶段所需关键信息不足，必须先进行简短澄清问答，再进行正式产出。

澄清问答应：
- 聚焦当前阶段最关键的不确定信息
- 每轮控制在 3~5 个问题内
- 优先使用选项、示例和对比帮助用户回答
- 避免一次性提出过多开放性问题

---

## Document Evolution Rule
项目文档是可迭代演进的，不要求第一次生成时即完整或最终定稿。

当项目形态发生变化时（例如：
- 从纯前端演进到全栈
- 从本地数据演进到持久化存储
- 从单用户工具演进到多用户协作）

相关文档必须被更新，以明确区分：
- 当前范围（Current Scope）
- 未来扩展（Future Extension）

---

## Missing Context Rule
若当前阶段所需关键输入文档不存在、不完整或彼此冲突，Agent 不应直接跳到实现。

应按以下顺序处理：
1. 明确指出缺失或冲突的上下文
2. 尝试从已有文档中提炼最小可行假设
3. 若假设风险较高，则先发起澄清问答
4. 在输出中显式标注假设及风险

---

## Global Rules
1. 先阅读 `docs/project-overview.md` 理解项目目标、范围和约束。

2. 需求阶段只允许输出产品文档，不允许直接写业务代码。

3. UI/UX 阶段负责：
   - 页面结构
   - 用户流程
   - 信息架构
   - 组件拆分
   - 状态设计（loading / empty / error）
   不负责具体代码实现。

4. 架构阶段只允许输出技术方案，不允许直接跳到完整实现。
   并应参考：
   - `docs/uiux-design.md`（如果存在）

5. 实现阶段必须基于：
   - `docs/architecture.md`
   - `docs/api-contracts.md`
   - `docs/engineering-guidelines.md`
   - `docs/task-board.md`
   - `docs/uiux-design.md`（如果存在）

6. 测试与审查阶段必须基于：
   - `docs/test-strategy.md`
   - 相关代码变更
   - 架构与接口契约

7. 一次只完成一个明确任务，不允许无边界扩展。

8. 发现需求、架构、代码三者冲突时：
   - 先列出冲突点
   - 再说明影响
   - 最后给出建议处理方案

9. 所有代码任务都必须：
   - 先说明实现思路
   - 列出假设
   - 再进行修改
   - 最后提供测试结果和未覆盖项

10. 默认优先：
   - 可维护性
   - 简洁性
   - 复用现有代码
   - 小步修改

11. 除非任务明确要求，否则不要：
   - 重构整个项目
   - 修改公共接口
   - 引入新基础设施
   - 替换核心技术栈

---

## Implementation Scope Rule
在实现阶段，Agent 必须严格限制在当前任务范围内。

默认不允许：
- 顺手修复无关问题
- 顺手重构相邻模块
- 在未获批准时扩展需求
- 在未更新文档前改变已确认契约

若发现结构性问题，应：
- 先记录问题
- 说明影响范围
- 提出建议
- 不直接进行大范围修改

---

## Required Output Structure
每次输出必须包含：

1. Role
2. Stage
3. Inputs Read
4. Assumptions
5. Output
6. Risks
7. Next Step

对于实现类任务，额外必须包含：

8. Change Summary
9. Validation
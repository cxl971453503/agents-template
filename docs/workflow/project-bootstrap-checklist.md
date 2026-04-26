# 项目初始化检查清单

## 目标
- 帮助 Codex 在复制模板后的第一次进入时判断当前是否仍是模板状态。
- 明确新项目启动前必须补齐的最小上下文。
- 避免把示例项目、模板占位或旧项目残留误认为当前项目事实。

## 使用时机
- 用户第一次在本模板中描述新项目想法时。
- `docs/project-overview.md`、`docs/product-requirements.md` 或 `docs/architecture.md` 不存在时。
- 当前仓库刚从模板复制而来，尚未生成真实项目文档时。
- Agent 对当前项目目标、技术栈或交付形态不确定时。

## 快速判断
如果以下任一项为“否”，应进入阶段 0：项目发现。

| 检查项 | 是 / 否 | 说明 |
| --- | --- | --- |
| `docs/project-overview.md` 是否存在且不是模板占位 |  | 项目目标是否明确 |
| `docs/product-requirements.md` 是否存在且不是模板占位 |  | MVP 范围是否明确 |
| `docs/architecture.md` 或 `docs/solution-design.md` 是否存在且不是模板占位 |  | 方案是否足够支持任务拆分 |
| 当前项目类型是否明确 |  | Web、CLI、数据项目、内容项目等 |
| 当前交付物是否明确 |  | 代码、文档、脚本、设计、数据、演示等 |
| 当前技术栈是否已确认或允许暂缓 |  | 不确定时不要硬猜 |
| 是否已区分当前范围与未来扩展 |  | 防止 MVP 失控 |
| `examples/` 是否仅作为参考 |  | 示例不得作为当前项目事实 |

## 初始化步骤
### 1. 识别模板状态
- 检查 `docs/` 根层是否缺少项目专属文档。
- 检查文档是否仍包含模板提示块。
- 检查用户是否只给出模糊项目想法。

### 2. 进入项目发现
由 PM Agent 发起简短问答，每轮最多 3~5 个问题，优先确认：
- 项目要解决什么问题
- 目标用户或使用者是谁
- 期望交付物是什么
- MVP 必须完成什么
- 当前有什么约束

### 3. 生成初始文档
信息足够后，从 `docs/template/` 生成：
- `docs/project-discovery.md`
- `docs/project-overview.md`
- `docs/product-requirements.md`
- `docs/architecture.md` 或 `docs/solution-design.md`

按需生成：
- `docs/uiux-design.md`
- `docs/api-contracts.md`
- `docs/test-strategy.md`

### 4. 判断项目类型
参考 `docs/workflow/project-type-guide.md`，确定当前项目更接近哪一类，并据此调整：
- 必备文档
- 任务拆分方式
- 测试策略
- 常见风险

### 5. 进入下一阶段
当项目目标、MVP 范围和基本方案足够清晰后，按 `docs/workflow/stage-handoff-template.md` 输出交接说明。

## 初始化输出建议
```md
1. 角色
- PM

2. 阶段
- 阶段 0：项目发现

3. 已读取输入
- AGENTS.md
- docs/workflow/project-bootstrap-checklist.md
- docs/template/*

4. 当前判断
- 当前仓库仍处于模板状态 / 已有真实项目上下文

5. 已确认信息
- ...

6. 不确定点
- ...

7. 本轮问题
1. ...

8. 下一步
- 根据用户回答生成初始项目文档
```

## 常见错误
- 直接把 `examples/acme-tasks/` 当成当前项目。
- 在用户只给出一句想法时直接进入实现。
- 在技术栈未确认时默认生成某个固定框架项目。
- 项目文档仍是模板占位，却进入任务规划。
- 未区分当前 MVP 和未来扩展。

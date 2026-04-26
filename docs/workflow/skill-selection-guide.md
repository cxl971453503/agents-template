# Skill 选择指南

## 目标
- 让 Skill 的引入有明确判断标准，而不是看到可用能力就默认启用。
- 保持模板轻量、通用，避免绑定某个技术栈、平台或工具生态。
- 帮助不同角色在正确阶段选择合适 Skill，并同步相关文档。

## 基本原则
1. 默认不启用强场景、强平台、强技术栈绑定的 Skill。
2. 只有当 Skill 能解决当前阶段的真实问题时，才建议启用。
3. 启用 Skill 前，应先说明它解决什么问题、依赖什么条件、为什么当前值得使用。
4. Skill 不应绕过阶段门禁。需求不清时，不能用实现类 Skill 直接开工。
5. 如果不启用 Skill 也能用现有模板完成任务，应优先保持简单。

## 角色职责
### PM
- 判断项目是否需要设计、图片、内容、表格、演示等特殊能力。
- 在阶段 0 或阶段 1 记录可能需要的 Skill，但不强行启用。

### Explorer
- 评估 Skill 与当前项目形态、技术栈、工具链和输入条件是否匹配。
- 输出是否建议启用，以及启用后的风险和替代方案。

### Builder
- 在任务已经明确后使用 Skill 完成具体产物。
- 若 Skill 改变产物结构、接口、设计流程或任务范围，必须同步文档。

### Tester
- 检查 Skill 生成的产物是否符合需求、方案、契约和测试策略。
- 对外部工具生成内容进行质量、边界和可维护性审查。

### Reporter
- 在阶段交接中记录本阶段启用过哪些 Skill、产生了哪些产物、剩余哪些风险。

## 阶段判断
| 阶段 | Skill 使用建议 |
| --- | --- |
| 阶段 0：项目发现 | 只记录潜在需求，不急于启用 |
| 阶段 1：产品定义 | 可判断是否需要设计、图像、表格、文档、演示等能力 |
| 阶段 1.5：体验与界面设计 | 可启用设计、图像、UI 相关 Skill |
| 阶段 2：方案设计 | 可评估技术栈相关 Skill 是否匹配 |
| 阶段 3：任务规划 | 将 Skill 使用拆入具体任务和完成定义 |
| 阶段 4：构建实现 | 在明确任务范围内使用 Skill 生成或修改产物 |
| 阶段 5：测试与评审 | 审查 Skill 产物质量和文档同步 |
| 阶段 6：交接与沉淀 | 记录 Skill 使用结果、风险和后续建议 |

## 推荐分级
### A 类：通用但按需启用
适合多数项目，但不一定每次都需要。

- `imagegen`：图片、插图、封面、Mockup、素材草图
- 表格类 Skill：Excel、CSV、数据整理
- 文档类 Skill：Word、PDF、Markdown 批处理
- 幻灯片类 Skill：汇报、路演、交付说明

### B 类：高价值但技术栈绑定
只有技术栈或工具链明确匹配时才启用。

- `shadcn-ui`：React + Tailwind UI 组件工程化
- `react:components`：React 组件拆分与落地
- API 契约类 Skill：OpenAPI、Swagger、接口生成
- E2E 测试类 Skill：Playwright 等测试自动化

### C 类：平台或生态绑定
仅在项目明确采用对应平台时启用。

- `design-md`
- `enhance-prompt`
- `stitch-loop`
- `remotion`

## 启用前检查清单
启用任何 Skill 前，至少回答：

1. 当前任务是否真的需要这个 Skill？
2. 当前阶段是否允许使用这个 Skill？
3. 项目技术栈、平台或输入条件是否满足？
4. Skill 产物会不会改变需求、方案、接口、任务或测试策略？
5. 如果 Skill 输出质量不稳定，是否有验证和回退方案？
6. 不使用该 Skill 是否已经足够完成当前任务？

## 文档同步
启用 Skill 后，按影响范围检查：

- 改变项目范围：更新 `docs/project-overview.md`
- 改变需求或验收标准：更新 `docs/product-requirements.md`
- 改变体验、页面或素材策略：更新 `docs/uiux-design.md`
- 改变方案或工具链：更新 `docs/architecture.md` 或 `docs/solution-design.md`
- 改变任务拆分：更新 `docs/task-board.md`
- 改变测试方式或交付门槛：更新 `docs/test-strategy.md`
- 改变长期规则：更新 `docs/workflow/engineering-guidelines.md` 或本文件

具体判断参考 `docs/workflow/document-sync-matrix.md`。

## 输出要求
当建议启用 Skill 时，输出中应包含：

```md
Skill 建议：
- Skill 名称：
- 使用阶段：
- 解决的问题：
- 依赖前提：
- 预期产物：
- 替代方案：
- 风险与验证方式：
```

当不建议启用 Skill 时，说明：

```md
暂不启用 Skill：
- 候选 Skill：
- 不启用原因：
- 当前替代做法：
- 后续触发条件：
```

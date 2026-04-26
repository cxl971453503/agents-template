# 接入已有项目指南

## 目标
- 帮助用户把本多智能体模板安全接入已有项目。
- 避免覆盖已有 `AGENTS.md`、`README.md`、`docs/` 或真实工程规则。
- 让 Codex 先理解现有项目，再决定如何补齐多 Agent 工作流。

## 适用场景
- 目标项目已经存在代码、文档或工程规范。
- 目标项目已有 `AGENTS.md`、`README.md`、`docs/`、测试命令或 CI 配置。
- 用户想把五角色流程、阶段门禁、文档同步和评审规则接入现有项目。

## 核心原则
1. 不覆盖已有项目事实源。
2. 先由 Explorer 扫描目标项目，再决定合并方式。
3. 通用模板规则应让位于目标项目的明确约束。
4. 模板文档应放在清晰位置，避免和真实项目文档混淆。
5. 接入完成后，应输出一次阶段 6：交接与沉淀说明。

## 推荐复制范围
### 通常可以复制
```text
.codex/agents/
.codex/prompts/
.codex/handoff/
docs/agents/
docs/template/
docs/workflow/
docs/optional-skills.md
```

### 需要谨慎合并
```text
AGENTS.md
README.md
docs/decisions/
```

### 通常不建议复制
```text
examples/
```

`examples/` 只用于模板仓库说明，不应进入大多数真实项目。若目标项目需要参考示例，可以单独复制到临时目录，并在完成后删除。

## 接入前检查
在复制或合并前，先检查目标项目：

| 检查项 | 处理建议 |
| --- | --- |
| 是否已有 `AGENTS.md` | 不覆盖，先合并 |
| 是否已有 `README.md` | 不覆盖，保留项目 README |
| 是否已有 `docs/` | 不覆盖真实项目文档 |
| 是否已有架构、需求、测试文档 | 映射到本模板阶段输入 |
| 是否已有编码规范或贡献规范 | 优先保留项目专属规范 |
| 是否已有 CI / 测试命令 | 写入工程规范或测试策略 |
| 是否已有任务管理方式 | 不强行替换，必要时建立映射 |

## 推荐接入步骤
### 1. 复制非冲突文件
优先复制：
- `.codex/agents/`
- `.codex/prompts/`
- `.codex/handoff/`
- `docs/agents/`
- `docs/template/`
- `docs/workflow/`

如果目标项目已有同名目录，应先比较内容，不直接覆盖。

### 2. 合并 `AGENTS.md`
如果目标项目没有 `AGENTS.md`，可以复制模板版。

如果目标项目已有 `AGENTS.md`，应合并：
- 保留目标项目的技术栈、测试命令、目录约束、代码风格和业务规则。
- 加入五角色模型、阶段检查、文档同步和评审流程。
- 明确优先级：
  - 项目专属规则优先
  - 通用多 Agent 流程其次
  - 示例内容不参与当前项目

建议新增一节：
```md
## 多智能体工作流
本项目采用 PM / Explorer / Builder / Tester / Reporter 五角色流程。
详细规则参考 docs/workflow/。
```

### 3. 保护项目 README
不要用模板 README 覆盖目标项目 README。

可在目标项目 README 中追加：
```md
## Agent 工作流
本项目使用 Codex 多智能体工作流，规则见 AGENTS.md 与 docs/workflow/。
```

### 4. 映射已有文档
把已有文档映射到本模板文档体系：

| 目标项目已有文档 | 可映射为 |
| --- | --- |
| 产品说明、需求说明 | `docs/product-requirements.md` |
| 项目介绍、愿景、范围 | `docs/project-overview.md` |
| 技术方案、系统设计 | `docs/architecture.md` 或 `docs/solution-design.md` |
| API 文档、OpenAPI、接口说明 | `docs/api-contracts.md` |
| 测试计划、QA 文档 | `docs/test-strategy.md` |
| 任务列表、Roadmap | `docs/task-board.md` |

如果目标项目已有不同命名，不必强制改名。可以在 `AGENTS.md` 中说明映射关系。

### 5. 首次接入扫描
接入后，先让 Codex 进入 Explorer 模式，而不是 PM 模式。

推荐启动语：
```text
请按 docs/workflow/adopt-into-existing-project.md，先进入 Explorer 模式扫描当前项目，识别已有文档、代码结构、测试命令、缺失上下文和接入风险。不要先改代码。
```

Explorer 输出应包含：
- 当前项目类型判断
- 已有文档清单
- 已有代码 / 产物结构
- 可映射到模板的文档
- 缺失的关键输入
- 与模板规则冲突的地方
- 建议的接入方案

### 6. 补齐缺失文档
根据 Explorer 输出，由 PM 或 Builder 补齐缺失文档。

优先补齐：
- `docs/project-overview.md`
- `docs/product-requirements.md`
- `docs/architecture.md` 或 `docs/solution-design.md`
- `docs/task-board.md`
- `docs/test-strategy.md`

不要为了满足模板而创建空文档。若暂时缺失，应写明“待补齐”和最小可行假设。

### 7. 交接沉淀
接入完成后，由 Reporter 输出：
- 已复制文件
- 已合并文件
- 未覆盖的项目文件
- 文档映射关系
- 当前缺失项
- 后续建议

## 冲突处理规则
当模板规则与目标项目规则冲突时：

1. 项目已有明确规则优先。
2. 安全、合规、测试、发布相关规则优先于通用流程便利性。
3. 若项目规则过期或互相冲突，先记录冲突和影响，再建议修改。
4. 不在未确认前替换技术栈、目录结构、测试框架或发布流程。

## 常见错误
- 直接覆盖目标项目 `AGENTS.md`。
- 用模板 README 覆盖项目 README。
- 把 `examples/` 复制进真实项目并让 Agent 误读。
- 目标项目已有文档，却强行重建一套重复文档。
- 还没扫描项目，就直接进入阶段 0 重新定义项目。
- 未记录已有文档和模板文档的映射关系。

## 接入完成检查
| 检查项 | 是否完成 |
| --- | --- |
| 已保护目标项目 README |  |
| 已合并或保留目标项目 AGENTS.md |  |
| 已复制 `.codex/agents/` |  |
| 已复制 `docs/agents/`、`docs/template/`、`docs/workflow/` |  |
| 已明确 `examples/` 不参与当前项目 |  |
| 已完成 Explorer 首次扫描 |  |
| 已记录文档映射关系 |  |
| 已列出缺失文档和风险 |  |
| 已输出接入交接说明 |  |

# 项目类型适配指南

## 目标
- 帮助 Agent 根据项目类型调整文档、任务、测试和风险关注点。
- 保持模板通用，同时避免所有项目都套同一种软件工程流程。
- 让 PM、Explorer、Builder、Tester 在不同项目形态下有稳定判断依据。

## 使用方式
项目发现或方案设计阶段，先判断项目最接近哪一类。若项目跨类型，应选择一个主类型，再记录次要类型。

输出中应说明：
- 主项目类型
- 次要项目类型（如果有）
- 因类型带来的文档、任务和测试调整

## 通用类型
### Web 应用
适用于：
- SaaS、管理后台、门户、内容站、Web 工具

必备文档：
- `docs/project-overview.md`
- `docs/product-requirements.md`
- `docs/uiux-design.md`
- `docs/architecture.md`
- `docs/api-contracts.md`（涉及后端或外部接口时）
- `docs/task-board.md`
- `docs/test-strategy.md`

常见任务：
- 页面与路由
- 组件与状态
- 数据模型与接口
- 认证与权限
- 表单与校验
- E2E 冒烟测试

测试重点：
- 核心用户路径
- 表单错误态
- 接口契约
- 响应式布局
- 权限边界

常见风险：
- 为了赶进度牺牲主流程体验
- API 契约和前端消费不一致
- 错误态、空状态和加载态遗漏

### CLI 工具
适用于：
- 命令行工具、开发者工具、批处理脚本

必备文档：
- `docs/project-overview.md`
- `docs/product-requirements.md`
- `docs/architecture.md` 或 `docs/solution-design.md`
- `docs/api-contracts.md`（用于命令、参数、文件格式契约）
- `docs/task-board.md`
- `docs/test-strategy.md`

常见任务：
- 命令设计
- 参数解析
- 文件读写
- 错误码与退出码
- 安装与使用说明

测试重点：
- 参数组合
- 文件不存在或格式错误
- 退出码
- 标准输出与错误输出
- 跨平台路径处理

常见风险：
- 命令语义不清
- 错误信息不可操作
- 路径和编码问题

### 数据分析项目
适用于：
- 数据清洗、指标分析、报表、可视化、实验分析

必备文档：
- `docs/project-overview.md`
- `docs/product-requirements.md`
- `docs/solution-design.md`
- `docs/api-contracts.md`（用于数据格式契约）
- `docs/task-board.md`
- `docs/test-strategy.md`

常见任务：
- 数据源确认
- 字段字典
- 清洗规则
- 指标口径
- 可视化输出
- 结果解释

测试重点：
- 样本数据
- 缺失值和异常值
- 指标计算口径
- 可复现性
- 输出文件格式

常见风险：
- 指标定义含糊
- 数据质量不足
- 结果不可复现

### 自动化脚本 / 工作流
适用于：
- 文件处理、定时任务、集成自动化、本地效率工具

必备文档：
- `docs/project-overview.md`
- `docs/product-requirements.md`
- `docs/solution-design.md`
- `docs/task-board.md`
- `docs/test-strategy.md`

常见任务：
- 输入输出定义
- 执行流程
- 配置管理
- 日志与错误处理
- 幂等与回滚策略

测试重点：
- 正常路径
- 重复执行
- 文件缺失
- 权限不足
- 外部服务失败

常见风险：
- 破坏性文件操作
- 错误重试导致重复副作用
- 缺少日志和可观察性

### 内容 / 文档项目
适用于：
- 课程、报告、知识库、手册、文章、规范文档

必备文档：
- `docs/project-overview.md`
- `docs/product-requirements.md`
- `docs/solution-design.md`
- `docs/task-board.md`

常见任务：
- 受众定义
- 目录结构
- 写作风格
- 内容来源
- 审校规则
- 发布格式

测试重点：
- 事实准确性
- 结构完整性
- 术语一致性
- 可读性
- 引用和版权风险

常见风险：
- 受众不明确
- 内容范围膨胀
- 术语前后不一致

### 游戏 / 模拟器
适用于：
- 游戏原型、策略模拟、交互沙盒、仿真工具

必备文档：
- `docs/project-overview.md`
- `docs/product-requirements.md`
- `docs/uiux-design.md`
- `docs/architecture.md`
- `docs/task-board.md`
- `docs/test-strategy.md`

常见任务：
- 核心玩法或模拟规则
- 状态模型
- 输入与反馈
- 渲染或表现
- 存档与回放（需要时）

测试重点：
- 核心循环
- 状态转移
- 边界条件
- 性能和帧率
- 主体验布局

常见风险：
- 规则不清导致实现漂移
- 主体验被侧边栏或配置面板吞掉
- 状态爆炸缺少测试

### AI Agent / 工作流项目
适用于：
- 多 Agent 系统、提示词工作流、自动化协作流程、工具调用链

必备文档：
- `docs/project-overview.md`
- `docs/product-requirements.md`
- `docs/solution-design.md`
- `docs/api-contracts.md`（用于工具、消息、状态契约）
- `docs/task-board.md`
- `docs/test-strategy.md`

常见任务：
- 角色定义
- 阶段门禁
- 工具权限
- 上下文传递
- 失败恢复
- 审计与日志

测试重点：
- 典型任务链路
- 工具调用边界
- 上下文缺失处理
- 错误恢复
- 输出格式稳定性

常见风险：
- 角色边界不清
- 上下文污染
- 工具权限过宽
- 输出不可验证

### 移动 / 桌面应用
适用于：
- 原生应用、跨平台应用、本地桌面工具

必备文档：
- `docs/project-overview.md`
- `docs/product-requirements.md`
- `docs/uiux-design.md`
- `docs/architecture.md`
- `docs/task-board.md`
- `docs/test-strategy.md`

常见任务：
- 平台能力
- 本地存储
- 离线状态
- 权限申请
- 安装与发布

测试重点：
- 平台兼容性
- 本地状态恢复
- 权限失败
- 性能和资源占用
- 安装升级流程

常见风险：
- 平台差异被低估
- 本地数据迁移缺少策略
- 权限和隐私说明不足

## 类型选择输出格式
```md
项目类型判断：
- 主类型：
- 次要类型：
- 判断依据：
- 必备文档调整：
- 测试策略调整：
- 主要风险：
```

## 混合项目处理
如果项目同时属于多类，按以下规则处理：
- 选择最影响交付方式的类型作为主类型。
- 选择最影响测试方式的类型作为次要类型。
- 若类型冲突，以用户目标和 MVP 范围为准。
- 不因混合类型自动扩大范围。

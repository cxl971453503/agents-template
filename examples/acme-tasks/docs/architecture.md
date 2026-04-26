# 架构设计

## 架构目标
- 快速交付 MVP
- 保持单体结构，避免过早拆分
- 前后端边界清晰
- 方便后续增加权限、通知和审计能力

## 约束与假设
- 当前为小团队开发，优先单体全栈方案
- 前端和后端都可放在 Next.js 项目内
- 数据库为 PostgreSQL
- 使用 Prisma 管理数据访问

## 系统概览
- Web 客户端：Next.js App Router
- 服务层：Next.js Route Handlers / Server Actions
- 持久化：PostgreSQL + Prisma
- 认证：基于 session 或 JWT 的简化认证方案
- 测试：单元测试 + API 集成测试 + 基础 E2E

## 核心模块
1. 认证
2. 工作区
3. 项目
4. 任务
5. 评论
6. 用户资料

## 模块边界
### 认证
负责注册、登录、登出、鉴权上下文注入。

### 工作区
负责工作区创建、成员关系管理（MVP 可先简化）。

### 项目
负责项目实体及其与工作区的关联。

### 任务
负责任务创建、编辑、查询、状态流转、指派。

### 评论
负责任务评论的创建与查询。

## 数据模型
### User
- id
- email
- passwordHash
- name
- createdAt
- updatedAt

### Workspace
- id
- name
- ownerId
- createdAt
- updatedAt

### WorkspaceMember
- id
- workspaceId
- userId
- role

### Project
- id
- workspaceId
- name
- description
- createdAt
- updatedAt

### Task
- id
- projectId
- title
- description
- status
- assigneeId
- creatorId
- dueDate
- createdAt
- updatedAt

### Comment
- id
- taskId
- authorId
- content
- createdAt

## 关键技术决策
1. 先使用单体全栈架构，而不是微服务。
2. 所有业务写入统一经过服务层，不直接在页面层写 Prisma。
3. API 返回结构保持统一，便于前端处理错误。
4. 状态字段使用枚举，避免自由字符串污染。

## 风险
- 若后续增加权限模型，当前简化成员设计可能要扩展。
- 任务筛选复杂度上升后，需要增加索引和查询优化。
- 若评论量变大，任务详情页需要分页。

## 回退 / 简化策略
- 若开发周期紧张，可先移除工作区成员管理，默认单工作区。
- 若 UI 复杂度过高，可先只做列表视图，不做看板视图。

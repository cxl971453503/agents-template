# Architecture

## Architecture Goals
- 快速交付 MVP
- 保持单体结构，避免过早拆分
- 前后端边界清晰
- 方便后续增加权限、通知和审计能力

## Constraints and Assumptions
- 当前为小团队开发，优先单体全栈方案
- 前端和后端都可放在 Next.js 项目内
- 数据库为 PostgreSQL
- 使用 Prisma 管理数据访问

## System Overview
- Web Client: Next.js App Router
- Server Layer: Next.js Route Handlers / Server Actions
- Persistence: PostgreSQL + Prisma
- Authentication: 基于 session 或 JWT 的简化认证方案
- Testing: 单元测试 + API 集成测试 + 基础 E2E

## Core Modules
1. Auth
2. Workspace
3. Project
4. Task
5. Comment
6. User Profile

## Module Boundaries
### Auth
负责注册、登录、登出、鉴权上下文注入。

### Workspace
负责工作区创建、成员关系管理（MVP 可先简化）。

### Project
负责项目实体及其与工作区的关联。

### Task
负责任务创建、编辑、查询、状态流转、指派。

### Comment
负责任务评论的创建与查询。

## Data Model
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

## Key Technical Decisions
1. 先使用单体全栈架构，而不是微服务。
2. 所有业务写入统一经过服务层，不直接在页面层写 Prisma。
3. API 返回结构保持统一，便于前端处理错误。
4. 状态字段使用枚举，避免自由字符串污染。

## Risks
- 若后续增加权限模型，当前简化成员设计可能要扩展。
- 任务筛选复杂度上升后，需要增加索引和查询优化。
- 若评论量变大，任务详情页需要分页。

## Rollback / Simplification Strategy
- 若开发周期紧张，可先移除工作区成员管理，默认单工作区。
- 若 UI 复杂度过高，可先只做列表视图，不做看板视图。
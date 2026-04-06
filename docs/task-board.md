# Task Board

## Milestone 1: Foundation
- T-001 初始化 Next.js 项目结构
- T-002 配置 Prisma 与 PostgreSQL
- T-003 建立基础用户认证流程
- T-004 建立统一 API 响应格式

## Milestone 2: Project & Task Core
- T-101 创建 Project 数据模型与 API
- T-102 创建 Task 数据模型与 API
- T-103 实现任务列表页
- T-104 实现任务创建表单
- T-105 实现任务编辑与状态更新

## Milestone 3: Collaboration
- T-201 实现 Comment 数据模型与 API
- T-202 实现任务详情页评论区
- T-203 实现按状态和负责人筛选

## Task Template
### Task ID
T-104

### Title
实现任务创建表单

### Goal
用户可以在项目页创建新任务并提交到后端。

### Inputs
- docs/architecture.md
- docs/api-contracts.md
- 现有 Project 页面结构

### Outputs
- 表单 UI
- 表单校验
- 调用任务创建 API
- 成功和失败反馈

### Dependencies
- T-102 已完成
- T-103 基础页面已存在

### Risks
- 表单字段与 API 契约不一致
- 错误态展示遗漏

### Definition of Done
- 可填写并提交
- 提交成功后列表更新
- 提交失败有提示
- 关键交互有测试覆盖
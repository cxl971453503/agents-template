# Project Overview

## Project Name
Acme Tasks

## Summary
一个面向小团队的任务管理 Web 应用，支持任务创建、分配、评论、状态跟踪和基础看板视图。

## Goal
帮助 5~50 人的小团队以更低成本管理协作任务，替代分散在聊天工具和表格中的任务记录。

## Target Users
- 小型创业团队
- 产品经理
- 研发团队
- 运营团队

## MVP Scope
- 用户注册 / 登录
- 工作区创建
- 项目创建
- 任务创建 / 编辑 / 指派 / 状态更新
- 评论
- 基础筛选与列表展示

## Non-goals
- 不做复杂权限系统
- 不做实时协作编辑
- 不做高级 BI 报表
- 不做企业级审计系统

## Constraints
- 团队规模：2~4 人
- 首个 MVP 开发周期：4 周
- 技术栈：Next.js + Prisma + PostgreSQL
- 优先快速上线，不追求复杂微服务拆分
- 默认部署在 Vercel / Docker 环境

## Success Criteria
- 用户可以在 5 分钟内创建工作区并建立第一个项目
- 任务完整流程可跑通：创建 -> 指派 -> 更新状态 -> 评论
- 关键页面首屏性能可接受
- 基础 E2E 冒烟测试通过
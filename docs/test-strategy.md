# Test Strategy

## Testing Goals
- 确保核心链路可用
- 降低回归风险
- 保证任务、项目、评论等关键模块的基本正确性

## Test Layers
### Unit Tests
覆盖：
- 状态流转逻辑
- 输入校验
- 服务层纯业务逻辑

### Integration Tests
覆盖：
- API 输入输出
- 数据库读写流程
- 权限边界（MVP 下为简化版本）

### E2E Smoke Tests
覆盖：
- 登录
- 创建项目
- 创建任务
- 更新任务状态
- 添加评论

## Priority
1. Auth
2. Task CRUD
3. Comment flow
4. Project listing

## Release Gate
发布前至少满足：
- 所有关键 API 测试通过
- 至少 1 条核心 E2E 路径通过
- 无阻塞级 bug
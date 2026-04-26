# API 契约

## 通用约定
- 所有响应均返回 JSON
- 成功响应：
  - `success: true`
  - `data: ...`
- 失败响应：
  - `success: false`
  - `error: { code, message }`

---

## POST /api/auth/login

### 请求
```json
{
  "email": "user@example.com",
  "password": "string"
}
```

### 响应
```json
{
  "success": true,
  "data": {
    "user": {
      "id": "u_123",
      "email": "user@example.com",
      "name": "Tom"
    }
  }
}
```

### 错误响应
```json
{
  "success": false,
  "error": {
    "code": "INVALID_CREDENTIALS",
    "message": "邮箱或密码错误。"
  }
}
```

---

## POST /api/projects

### 请求
```json
{
  "workspaceId": "w_123",
  "name": "官网改版",
  "description": "项目描述"
}
```

### 响应
```json
{
  "success": true,
  "data": {
    "id": "p_123",
    "workspaceId": "w_123",
    "name": "官网改版",
    "description": "项目描述"
  }
}
```

### 错误响应
```json
{
  "success": false,
  "error": {
    "code": "INVALID_INPUT",
    "message": "项目名称不能为空。"
  }
}
```

---

## POST /api/tasks

### 请求
```json
{
  "projectId": "p_123",
  "title": "实现登录页",
  "description": "完成界面与校验",
  "assigneeId": "u_2",
  "dueDate": "2026-04-10"
}
```

### 响应
```json
{
  "success": true,
  "data": {
    "id": "t_123",
    "projectId": "p_123",
    "title": "实现登录页",
    "description": "完成界面与校验",
    "assigneeId": "u_2",
    "dueDate": "2026-04-10",
    "status": "TODO"
  }
}
```

### 错误响应
```json
{
  "success": false,
  "error": {
    "code": "PROJECT_NOT_FOUND",
    "message": "指定的项目不存在。"
  }
}
```

---

## PATCH /api/tasks/:id

### 请求
```json
{
  "title": "更新后的标题",
  "description": "更新后的描述",
  "status": "IN_PROGRESS",
  "assigneeId": "u_2"
}
```

### 响应
```json
{
  "success": true,
  "data": {
    "id": "t_123",
    "title": "更新后的标题",
    "description": "更新后的描述",
    "status": "IN_PROGRESS",
    "assigneeId": "u_2"
  }
}
```

### 错误响应
```json
{
  "success": false,
  "error": {
    "code": "TASK_NOT_FOUND",
    "message": "指定的任务不存在。"
  }
}
```

---

## GET /api/tasks?projectId=p_123&status=TODO

### 响应
```json
{
  "success": true,
  "data": [
    {
      "id": "t_123",
      "title": "实现登录页",
      "status": "TODO",
      "assigneeId": "u_2",
      "dueDate": "2026-04-10"
    },
    {
      "id": "t_124",
      "title": "添加密码校验",
      "status": "TODO",
      "assigneeId": "u_3",
      "dueDate": "2026-04-11"
    }
  ]
}
```

### 错误响应
```json
{
  "success": false,
  "error": {
    "code": "INVALID_QUERY",
    "message": "查询参数不合法。"
  }
}
```

---

## POST /api/tasks/:id/comments

### 请求
```json
{
  "content": "请调整一下界面文案。"
}
```

### 响应
```json
{
  "success": true,
  "data": {
    "id": "c_123",
    "taskId": "t_123",
    "authorId": "u_2",
    "content": "请调整一下界面文案。",
    "createdAt": "2026-04-06T10:00:00Z"
  }
}
```

### 错误响应
```json
{
  "success": false,
  "error": {
    "code": "TASK_NOT_FOUND",
    "message": "任务不存在，无法添加评论。"
  }
}
```

---

## 建议统一使用的错误码

### 认证相关
- `UNAUTHORIZED`
- `INVALID_CREDENTIALS`

### 校验相关
- `INVALID_INPUT`
- `INVALID_QUERY`

### 资源相关错误
- `TASK_NOT_FOUND`
- `PROJECT_NOT_FOUND`
- `WORKSPACE_NOT_FOUND`
- `USER_NOT_FOUND`

### 权限相关错误
- `FORBIDDEN`

### 服务端错误
- `INTERNAL_SERVER_ERROR`

---

## 说明
- 所有日期建议使用 ISO 8601 格式。
- 所有 ID 字段目前示例使用字符串。
- `PATCH /api/tasks/:id` 支持部分更新，不要求每个字段都传。
- 后续如果加入分页，建议统一返回：
  - `items`
  - `page`
  - `pageSize`
  - `total`

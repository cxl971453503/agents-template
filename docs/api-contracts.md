# API Contracts

## General Conventions
- 所有响应均返回 JSON
- 成功响应：
  - `success: true`
  - `data: ...`
- 失败响应：
  - `success: false`
  - `error: { code, message }`

---

## POST /api/auth/login

### Request
```json
{
  "email": "user@example.com",
  "password": "string"
}
```

### Response
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

### Error Response
```json
{
  "success": false,
  "error": {
    "code": "INVALID_CREDENTIALS",
    "message": "Email or password is incorrect."
  }
}
```

---

## POST /api/projects

### Request
```json
{
  "workspaceId": "w_123",
  "name": "Website Revamp",
  "description": "Project description"
}
```

### Response
```json
{
  "success": true,
  "data": {
    "id": "p_123",
    "workspaceId": "w_123",
    "name": "Website Revamp",
    "description": "Project description"
  }
}
```

### Error Response
```json
{
  "success": false,
  "error": {
    "code": "INVALID_INPUT",
    "message": "Project name is required."
  }
}
```

---

## POST /api/tasks

### Request
```json
{
  "projectId": "p_123",
  "title": "Implement login page",
  "description": "Build UI and validation",
  "assigneeId": "u_2",
  "dueDate": "2026-04-10"
}
```

### Response
```json
{
  "success": true,
  "data": {
    "id": "t_123",
    "projectId": "p_123",
    "title": "Implement login page",
    "description": "Build UI and validation",
    "assigneeId": "u_2",
    "dueDate": "2026-04-10",
    "status": "TODO"
  }
}
```

### Error Response
```json
{
  "success": false,
  "error": {
    "code": "PROJECT_NOT_FOUND",
    "message": "The specified project does not exist."
  }
}
```

---

## PATCH /api/tasks/:id

### Request
```json
{
  "title": "Updated title",
  "description": "Updated desc",
  "status": "IN_PROGRESS",
  "assigneeId": "u_2"
}
```

### Response
```json
{
  "success": true,
  "data": {
    "id": "t_123",
    "title": "Updated title",
    "description": "Updated desc",
    "status": "IN_PROGRESS",
    "assigneeId": "u_2"
  }
}
```

### Error Response
```json
{
  "success": false,
  "error": {
    "code": "TASK_NOT_FOUND",
    "message": "The specified task does not exist."
  }
}
```

---

## GET /api/tasks?projectId=p_123&status=TODO

### Response
```json
{
  "success": true,
  "data": [
    {
      "id": "t_123",
      "title": "Implement login page",
      "status": "TODO",
      "assigneeId": "u_2",
      "dueDate": "2026-04-10"
    },
    {
      "id": "t_124",
      "title": "Add password validation",
      "status": "TODO",
      "assigneeId": "u_3",
      "dueDate": "2026-04-11"
    }
  ]
}
```

### Error Response
```json
{
  "success": false,
  "error": {
    "code": "INVALID_QUERY",
    "message": "Query parameters are invalid."
  }
}
```

---

## POST /api/tasks/:id/comments

### Request
```json
{
  "content": "Please update the UI copy."
}
```

### Response
```json
{
  "success": true,
  "data": {
    "id": "c_123",
    "taskId": "t_123",
    "authorId": "u_2",
    "content": "Please update the UI copy.",
    "createdAt": "2026-04-06T10:00:00Z"
  }
}
```

### Error Response
```json
{
  "success": false,
  "error": {
    "code": "TASK_NOT_FOUND",
    "message": "Cannot add comment because task does not exist."
  }
}
```

---

## Suggested Common Error Codes

### Authentication
- `UNAUTHORIZED`
- `INVALID_CREDENTIALS`

### Validation
- `INVALID_INPUT`
- `INVALID_QUERY`

### Resource Errors
- `TASK_NOT_FOUND`
- `PROJECT_NOT_FOUND`
- `WORKSPACE_NOT_FOUND`
- `USER_NOT_FOUND`

### Permission Errors
- `FORBIDDEN`

### Server Errors
- `INTERNAL_SERVER_ERROR`

---

## Notes
- 所有日期建议使用 ISO 8601 格式。
- 所有 ID 字段目前示例使用字符串。
- `PATCH /api/tasks/:id` 支持部分更新，不要求每个字段都传。
- 后续如果加入分页，建议统一返回：
  - `items`
  - `page`
  - `pageSize`
  - `total`
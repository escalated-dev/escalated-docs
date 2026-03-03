# 状态和优先级

Escalated将工单视为状态机。状态转换是强制的且可配置。

## 状态

- Open
- In Progress
- Waiting on Customer
- Waiting on Agent
- Escalated
- Resolved
- Closed
- Reopened

## 优先级

- Low
- Medium
- High
- Urgent
- Critical

转换可在`config/escalated.php`的`transitions`键下进行配置。

管理员可以在管理面板（`/support/admin/statuses`）中创建和管理自定义状态。

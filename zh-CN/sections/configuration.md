# 配置

Escalated开箱即用，具有合理的默认值。配置是可选的，但可以自定义。

> **配置选项**
>
> - `routes.prefix` -- 所有Escalated路由的URL前缀（默认：`support`）
> - `routes.middleware` -- 应用于客户路由的中间件（默认：`['web', 'auth']`）
> - `user_model` -- 用户模型类（默认：`App\Models\User`）
> - `table_prefix` -- 数据库表前缀（默认：`escalated_`）
> - `tickets.allow_customer_close` -- 客户是否可以关闭自己的工单（默认：`true`）
> - `tickets.auto_close_resolved_after_days` -- 已解决工单在N天后自动关闭（默认：`7`）
> - `sla.business_hours_only` -- SLA目标仅计算工作时间（默认：`false`）
> - `notifications.channels` -- 通知渠道（默认：`['mail', 'database']`）

## 管理设置和模块

最近的平台更新添加了以下配置和管理界面：

- 具有条件显示规则的自定义字段
- 自定义状态和工作时间计划
- 角色（RBAC）、基于技能的路由和客服容量
- 审计日志查看
- 自动化和出站Webhook
- CSAT调查行为
- SSO和双因素认证
- 数据保留策略和清理行为
- 邮件渠道设置
- 自定义对象和记录

## 发布资源

```bash
# 发布配置文件
$ php artisan vendor:publish --tag=escalated-config

# 发布邮件模板以进行自定义
$ php artisan vendor:publish --tag=escalated-views

# 发布迁移文件（如需自定义）
$ php artisan vendor:publish --tag=escalated-migrations
```

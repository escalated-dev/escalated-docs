# 路由

Escalated在配置的前缀（默认：`/support`）下注册三组路由。

## 客户路由

| 方法 | URL | 说明 |
| ------ | --- | ----------- |
| GET | /support | 客户工单列表 |
| GET | /support/create | 新建工单表单 |
| POST | /support | 创建工单 |
| GET | /support/kb | 知识库首页 |
| GET | /support/kb/{slug} | 知识库文章 |
| POST | /support/kb/{slug}/feedback | 文章反馈 |
| GET | /support/{reference} | 工单详情 |
| POST | /support/{reference}/reply | 回复工单 |
| POST | /support/{reference}/close | 关闭工单 |
| POST | /support/{reference}/reopen | 重新打开工单 |
| POST | /support/{reference}/rate | 提交满意度评分 |

## 客服路由

需要`escalated-agent`门禁。

| 方法 | URL | 说明 |
| ------ | --- | ----------- |
| GET | /support/agent | 客服仪表板 |
| GET | /support/agent/tickets | 工单队列 |
| GET | /support/agent/tickets/{reference} | 工单详情 |
| POST | /support/agent/tickets/{reference}/reply | 公开回复 |
| POST | /support/agent/tickets/{reference}/note | 内部备注 |
| POST | /support/agent/tickets/{reference}/assign | 分配客服 |
| POST | /support/agent/tickets/{reference}/status | 更改状态 |
| POST | /support/agent/tickets/{reference}/priority | 更改优先级 |
| POST | /support/agent/tickets/bulk | 工单批量操作 |
| POST | /support/agent/tickets/{reference}/follow | 切换关注 |
| POST | /support/agent/tickets/{reference}/macro | 应用宏 |
| POST | /support/agent/tickets/{reference}/presence | 报告在线状态 |
| POST | /support/agent/tickets/{reference}/typing | 报告输入状态 |
| POST | /support/agent/tickets/{reference}/replies/{reply}/pin | 切换备注置顶 |

## 管理员路由

需要`escalated-admin`门禁。管理员拥有所有客服路由以及管理页面的访问权限。

| 方法 | URL | 说明 |
| ------ | --- | ----------- |
| GET | /support/admin/reports | 分析仪表板 |
| GET | /support/admin/departments | 部门管理 |
| GET | /support/admin/sla-policies | SLA策略管理 |
| GET | /support/admin/escalation-rules | 升级规则构建器 |
| GET | /support/admin/tags | 标签管理 |
| GET | /support/admin/canned-responses | 预设回复模板 |
| GET | /support/admin/macros | 宏管理 |
| GET | /support/admin/custom-fields | 自定义字段和表单 |
| GET | /support/admin/statuses | 自定义状态 |
| GET | /support/admin/business-hours | 工作时间计划 |
| GET | /support/admin/roles | 客服角色和权限 |
| GET | /support/admin/audit-log | 审计追踪 |
| GET | /support/admin/skills | 技能管理 |
| GET | /support/admin/capacity | 客服容量控制 |
| GET | /support/admin/automations | 基于时间的自动化 |
| GET | /support/admin/webhooks | 出站Webhook |
| GET | /support/admin/webhooks/{webhook}/deliveries | Webhook发送日志 |
| GET | /support/admin/kb-articles | 知识库文章 |
| GET | /support/admin/kb-categories | 知识库分类 |
| GET | /support/admin/reports/dashboard | 报表仪表板 |
| GET | /support/admin/reports/agents | 客服生产力报表 |
| GET | /support/admin/reports/sla | SLA达成报表 |
| GET | /support/admin/reports/csat | CSAT报表 |
| GET | /support/admin/settings/csat | CSAT调查设置 |
| GET | /support/admin/settings/sso | SSO设置 |
| GET | /support/admin/settings/two-factor | 双因素认证设置 |
| GET | /support/admin/settings/data-retention | 数据保留设置 |
| GET | /support/admin/settings/email | 邮件渠道设置 |
| GET | /support/admin/custom-objects | 自定义对象 |
| GET | /support/admin/custom-objects/{customObject}/records | 自定义对象记录 |
| GET | /support/admin/tickets/merge-search | 搜索合并目标 |
| POST | /support/admin/tickets/{reference}/merge | 将工单合并到目标 |
| GET | /support/admin/tickets/{reference}/links | 已关联工单列表 |
| POST | /support/admin/tickets/{reference}/links | 关联相关工单 |
| DELETE | /support/admin/tickets/{reference}/links/{link} | 取消关联工单 |
| GET | /support/admin/tickets/{reference}/side-conversations | 侧边对话列表 |
| POST | /support/admin/tickets/{reference}/side-conversations | 发起侧边对话 |
| POST | /support/admin/tickets/{reference}/side-conversations/{sideConversation}/reply | 回复侧边对话 |
| POST | /support/admin/tickets/{reference}/side-conversations/{sideConversation}/close | 关闭侧边对话 |
| POST | /support/admin/macros | 创建宏 |
| PUT | /support/admin/macros/{macro} | 更新宏 |
| DELETE | /support/admin/macros/{macro} | 删除宏 |

## 访客路由

无需认证。通过唯一令牌访问。

| 方法 | URL | 说明 |
| ------ | --- | ----------- |
| GET | /support/guest/create | 访客工单表单 |
| POST | /support/guest | 创建访客工单 |
| GET | /support/guest/{token} | 查看访客工单 |
| POST | /support/guest/{token}/reply | 回复访客工单 |
| POST | /support/guest/{token}/rate | 提交满意度评分 |

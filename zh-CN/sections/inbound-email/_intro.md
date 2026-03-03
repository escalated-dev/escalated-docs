# 入站邮件

直接从收到的邮件创建和回复工单。Escalated支持**Mailgun**、**Postmark**、**AWS SES** Webhook以及作为备用方案的**IMAP**轮询。

## 工作原理

1. 您的邮件提供商在您的支持地址（例如`support@yourapp.com`）收到邮件
2. 提供商通过Webhook将邮件转发到您的应用（或通过IMAP轮询获取）
3. Escalated规范化载荷并通过主题引用（例如`[ESC-00001]`）或`In-Reply-To`头部检查线程匹配
4. 匹配的邮件添加回复；不匹配的邮件创建新工单（未知发件人创建访客工单）

## 配置

在管理设置中启用入站邮件并配置适配器，或通过环境变量进行配置。管理设置优先于环境变量/配置文件的值。

## Webhook URL

将您的邮件提供商的入站Webhook指向以下URL。这些路由不需要认证（使用签名验证代替）。

| 提供商 | Webhook URL |
| --- | --- |
| Mailgun | `POST /support/inbound/mailgun` |
| Postmark | `POST /support/inbound/postmark` |
| AWS SES | `POST /support/inbound/ses` |

## IMAP轮询

对于不支持Webhook的邮件提供商，请在计划任务中使用IMAP轮询命令。

## 功能

- 通过主题引用和In-Reply-To / References头部进行**线程检测**
- 为未知发件人创建**访客工单**，自动推导显示名称
- 邮件回复到达时**自动重新打开**已解决或已关闭的工单
- 通过Message-ID头部进行**重复检测**，防止重复处理
- 可配置大小和数量限制的**附件处理**
- **审计日志**——每封入站邮件都被记录，用于调试和合规
- **管理员可配置**——所有设置可从管理面板管理，支持环境变量/配置文件回退

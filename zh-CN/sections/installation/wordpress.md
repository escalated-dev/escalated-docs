## 1. 安装插件

```bash
$ wp plugin install escalated --activate
```

## 2. 配置设置

在wp-admin中导航到**Escalated -> Settings**来配置部门、SLA策略、升级规则和邮件渠道。

## 3. 添加短代码

在任意页面放置短代码为客户提供支持门户：

```shortcodes
[escalated_tickets]        // Ticket list
[escalated_create_ticket]  // New ticket form
[escalated_view_ticket]    // Ticket detail
```

> **注意：** WordPress插件是自包含的——不使用Inertia.js。所有UI通过原生WordPress管理界面和基于短代码的前端模板渲染。

# التكوين

يعمل Escalated فور التثبيت بإعدادات افتراضية مناسبة. التكوين اختياري ولكنه متاح للتخصيص.

> **خيارات التكوين**
>
> - `routes.prefix` -- بادئة URL لجميع مسارات Escalated (الافتراضي: `support`)
> - `routes.middleware` -- الوسيطات المطبقة على مسارات العملاء (الافتراضي: `['web', 'auth']`)
> - `user_model` -- فئة نموذج المستخدم (الافتراضي: `App\Models\User`)
> - `table_prefix` -- بادئة جداول قاعدة البيانات (الافتراضي: `escalated_`)
> - `tickets.allow_customer_close` -- ما إذا كان يمكن للعملاء إغلاق تذاكرهم (الافتراضي: `true`)
> - `tickets.auto_close_resolved_after_days` -- إغلاق التذاكر المحلولة تلقائيًا بعد N يوم (الافتراضي: `7`)
> - `sla.business_hours_only` -- احتساب ساعات العمل فقط لأهداف SLA (الافتراضي: `false`)
> - `notifications.channels` -- قنوات الإشعارات (الافتراضي: `['mail', 'database']`)

## إعدادات الإدارة والوحدات

تضيف التحديثات الأخيرة للمنصة شاشات تكوين وإدارة لـ:

- حقول مخصصة مع قواعد إظهار شرطية
- حالات مخصصة وجداول ساعات العمل
- أدوار (RBAC)، توجيه قائم على المهارات، وسعة الوكلاء
- مراجعة سجل التدقيق
- الأتمتة وخطافات الويب الصادرة
- سلوك استبيان CSAT
- SSO والمصادقة الثنائية
- سياسات الاحتفاظ بالبيانات وسلوك الحذف
- إعدادات قنوات البريد الإلكتروني
- الكائنات المخصصة والسجلات

## نشر الأصول

```bash
# Publish config file
$ php artisan vendor:publish --tag=escalated-config

# Publish email templates for customization
$ php artisan vendor:publish --tag=escalated-views

# Publish migrations (if you need to customize)
$ php artisan vendor:publish --tag=escalated-migrations
```

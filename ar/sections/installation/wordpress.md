## 1. تثبيت الإضافة

```bash
$ wp plugin install escalated --activate
```

## 2. تكوين الإعدادات

انتقل إلى **Escalated -> Settings** في wp-admin لتكوين الأقسام وسياسات SLA وقواعد التصعيد وقنوات البريد الإلكتروني.

## 3. إضافة الأكواد القصيرة

ضع الأكواد القصيرة في أي صفحة لمنح العملاء بوابة دعم:

```shortcodes
[escalated_tickets]        // Ticket list
[escalated_create_ticket]  // New ticket form
[escalated_view_ticket]    // Ticket detail
```

> **ملاحظة:** إضافة WordPress مستقلة بذاتها -- لا تستخدم Inertia.js. تُعرض جميع الواجهات عبر شاشات إدارة WordPress الأصلية وقوالب الواجهة الأمامية المدعومة بالأكواد القصيرة.

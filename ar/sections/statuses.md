# الحالات والأولويات

يتعامل Escalated مع التذاكر كآلات حالة. يتم فرض انتقالات الحالة وهي قابلة للتكوين.

## الحالات

- Open
- In Progress
- Waiting on Customer
- Waiting on Agent
- Escalated
- Resolved
- Closed
- Reopened

## الأولويات

- Low
- Medium
- High
- Urgent
- Critical

يمكن تكوين الانتقالات عبر `config/escalated.php` تحت مفتاح `transitions`.

يمكن للمسؤولين إنشاء وإدارة حالات مخصصة في لوحة الإدارة (`/support/admin/statuses`).

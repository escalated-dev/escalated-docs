# الجدولة

يوفر Escalated أوامر artisan لإدارة دورة حياة التذاكر تلقائيًا. أضفها إلى المجدول الخاص بك.

```php
use Illuminate\Support\Facades\Schedule;

// Check for SLA breaches
Schedule::command('escalated:check-sla')->everyMinute();

// Evaluate escalation rules
Schedule::command('escalated:evaluate-escalations')->everyFiveMinutes();

// Run time-based automations
Schedule::command('escalated:run-automations')->everyFiveMinutes();

// Auto-close resolved tickets after configured days
Schedule::command('escalated:close-resolved')->daily();

// Purge old activity log entries
Schedule::command('escalated:purge-activities')->weekly();

// Purge data according to retention settings
Schedule::command('escalated:purge-expired')->daily();

// Poll inbound IMAP mailbox (only if using IMAP inbound adapter)
Schedule::command('escalated:poll-imap')->everyMinute();
```

## الأوامر المتاحة

- `escalated:check-sla` -- يتحقق من التذاكر المفتوحة مقابل سياسات SLA ويرسل أحداث `SlaBreached`
- `escalated:evaluate-escalations` -- يشغل قواعد التصعيد ضد التذاكر المطابقة ويطبق الإجراءات المُعدة
- `escalated:run-automations` -- يشغل قواعد الأتمتة المبنية على الوقت ضد التذاكر المؤهلة
- `escalated:close-resolved` -- يغلق التذاكر التي كانت في حالة "resolved" لعدد الأيام المُعد
- `escalated:purge-activities` -- يحذف إدخالات سجل النشاط الأقدم من فترة الاحتفاظ المُعدة
- `escalated:purge-expired` -- يحذف التذاكر والمرفقات وسجلات التدقيق بناءً على إعدادات سياسة الاحتفاظ
- `escalated:poll-imap` -- يستطلع صندوق بريد IMAP المُعد للبريد الوارد

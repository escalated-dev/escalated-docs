```php
use Escalated\Laravel\Events\TicketCreated;

Event::listen(TicketCreated::class, function ($event) {
    // $event->ticket
});
```

**الأحداث المتاحة**

- `TicketCreated` -- تذكرة جديدة مقدمة
- `TicketStatusChanged` -- انتقال الحالة
- `TicketPriorityChanged` -- تحديث الأولوية
- `TicketAssigned` -- تعيين وكيل للتذكرة
- `TicketUnassigned` -- إزالة وكيل من التذكرة
- `ReplyCreated` -- إضافة رد عام
- `InternalNoteAdded` -- ملاحظة داخلية للوكيل
- `TicketUpdated` -- تغيير بيانات التذكرة الوصفية
- `TicketReopened` -- إعادة التذكرة إلى الحالة النشطة
- `DepartmentChanged` -- إعادة تعيين القسم
- `TagAddedToTicket` -- تطبيق وسم على التذكرة
- `TagRemovedFromTicket` -- إزالة وسم من التذكرة
- `SlaWarning` -- التذكرة تقترب من موعد SLA النهائي
- `SlaBreached` -- تجاوز موعد SLA النهائي
- `TicketEscalated` -- تصعيد التذكرة بواسطة قاعدة
- `TicketResolved` -- تحديد التذكرة كمحلولة
- `TicketClosed` -- إغلاق التذكرة

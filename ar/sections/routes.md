# المسارات

يسجل Escalated ثلاث مجموعات من المسارات تحت البادئة المُعدة (الافتراضي: `/support`).

## مسارات العملاء

| الطريقة | الرابط | الوصف |
| ------ | --- | ----------- |
| GET | /support | قائمة تذاكر العميل |
| GET | /support/create | نموذج تذكرة جديدة |
| POST | /support | إنشاء تذكرة |
| GET | /support/kb | الصفحة الرئيسية لقاعدة المعرفة |
| GET | /support/kb/{slug} | مقال قاعدة المعرفة |
| POST | /support/kb/{slug}/feedback | تقييم المقال |
| GET | /support/{reference} | تفاصيل التذكرة |
| POST | /support/{reference}/reply | الرد على التذكرة |
| POST | /support/{reference}/close | إغلاق التذكرة |
| POST | /support/{reference}/reopen | إعادة فتح التذكرة |
| POST | /support/{reference}/rate | إرسال تقييم الرضا |

## مسارات الوكلاء

يتطلب بوابة `escalated-agent`.

| الطريقة | الرابط | الوصف |
| ------ | --- | ----------- |
| GET | /support/agent | لوحة تحكم الوكيل |
| GET | /support/agent/tickets | قائمة انتظار التذاكر |
| GET | /support/agent/tickets/{reference} | تفاصيل التذكرة |
| POST | /support/agent/tickets/{reference}/reply | رد عام |
| POST | /support/agent/tickets/{reference}/note | ملاحظة داخلية |
| POST | /support/agent/tickets/{reference}/assign | تعيين وكيل |
| POST | /support/agent/tickets/{reference}/status | تغيير الحالة |
| POST | /support/agent/tickets/{reference}/priority | تغيير الأولوية |
| POST | /support/agent/tickets/bulk | إجراءات جماعية على التذاكر |
| POST | /support/agent/tickets/{reference}/follow | تبديل المتابعة |
| POST | /support/agent/tickets/{reference}/macro | تطبيق ماكرو |
| POST | /support/agent/tickets/{reference}/presence | الإبلاغ عن الحضور |
| POST | /support/agent/tickets/{reference}/typing | الإبلاغ عن حالة الكتابة |
| POST | /support/agent/tickets/{reference}/replies/{reply}/pin | تبديل تثبيت الملاحظة |

## مسارات الإدارة

يتطلب بوابة `escalated-admin`. يمتلك المسؤولون جميع مسارات الوكلاء بالإضافة إلى صفحات الإدارة.

| الطريقة | الرابط | الوصف |
| ------ | --- | ----------- |
| GET | /support/admin/reports | لوحة التحليلات |
| GET | /support/admin/departments | إدارة الأقسام |
| GET | /support/admin/sla-policies | إدارة سياسات SLA |
| GET | /support/admin/escalation-rules | منشئ قواعد التصعيد |
| GET | /support/admin/tags | إدارة الوسوم |
| GET | /support/admin/canned-responses | قوالب الردود الجاهزة |
| GET | /support/admin/macros | إدارة الماكرو |
| GET | /support/admin/custom-fields | الحقول والنماذج المخصصة |
| GET | /support/admin/statuses | الحالات المخصصة |
| GET | /support/admin/business-hours | جداول ساعات العمل |
| GET | /support/admin/roles | أدوار وصلاحيات الوكلاء |
| GET | /support/admin/audit-log | سجل التدقيق |
| GET | /support/admin/skills | إدارة المهارات |
| GET | /support/admin/capacity | ضوابط سعة الوكلاء |
| GET | /support/admin/automations | الأتمتة المبنية على الوقت |
| GET | /support/admin/webhooks | خطافات الويب الصادرة |
| GET | /support/admin/webhooks/{webhook}/deliveries | سجل تسليم خطافات الويب |
| GET | /support/admin/kb-articles | مقالات قاعدة المعرفة |
| GET | /support/admin/kb-categories | تصنيفات قاعدة المعرفة |
| GET | /support/admin/reports/dashboard | لوحة التقارير |
| GET | /support/admin/reports/agents | تقرير إنتاجية الوكلاء |
| GET | /support/admin/reports/sla | تقرير تحقيق SLA |
| GET | /support/admin/reports/csat | تقرير CSAT |
| GET | /support/admin/settings/csat | إعدادات استبيان CSAT |
| GET | /support/admin/settings/sso | إعدادات SSO |
| GET | /support/admin/settings/two-factor | إعدادات المصادقة الثنائية |
| GET | /support/admin/settings/data-retention | إعدادات الاحتفاظ بالبيانات |
| GET | /support/admin/settings/email | إعدادات قناة البريد الإلكتروني |
| GET | /support/admin/custom-objects | الكائنات المخصصة |
| GET | /support/admin/custom-objects/{customObject}/records | سجلات الكائنات المخصصة |
| GET | /support/admin/tickets/merge-search | البحث عن أهداف الدمج |
| POST | /support/admin/tickets/{reference}/merge | دمج التذكرة في الهدف |
| GET | /support/admin/tickets/{reference}/links | قائمة التذاكر المرتبطة |
| POST | /support/admin/tickets/{reference}/links | ربط تذكرة ذات صلة |
| DELETE | /support/admin/tickets/{reference}/links/{link} | إلغاء ربط تذكرة ذات صلة |
| GET | /support/admin/tickets/{reference}/side-conversations | قائمة المحادثات الجانبية |
| POST | /support/admin/tickets/{reference}/side-conversations | بدء محادثة جانبية |
| POST | /support/admin/tickets/{reference}/side-conversations/{sideConversation}/reply | الرد في محادثة جانبية |
| POST | /support/admin/tickets/{reference}/side-conversations/{sideConversation}/close | إغلاق محادثة جانبية |
| POST | /support/admin/macros | إنشاء ماكرو |
| PUT | /support/admin/macros/{macro} | تحديث ماكرو |
| DELETE | /support/admin/macros/{macro} | حذف ماكرو |

## مسارات الضيوف

لا تتطلب مصادقة. يتم الوصول عبر رمز فريد.

| الطريقة | الرابط | الوصف |
| ------ | --- | ----------- |
| GET | /support/guest/create | نموذج تذكرة الضيف |
| POST | /support/guest | إنشاء تذكرة ضيف |
| GET | /support/guest/{token} | عرض تذكرة الضيف |
| POST | /support/guest/{token}/reply | الرد على تذكرة الضيف |
| POST | /support/guest/{token}/rate | إرسال تقييم الرضا |

# Durumlar ve Öncelikler

Escalated, biletleri durum makineleri olarak ele alır. Durum geçişleri zorunludur ve yapılandırılabilir.

## Durumlar

- Open
- In Progress
- Waiting on Customer
- Waiting on Agent
- Escalated
- Resolved
- Closed
- Reopened

## Öncelikler

- Low
- Medium
- High
- Urgent
- Critical

Geçişler `config/escalated.php` dosyasında `transitions` anahtarı altında yapılandırılabilir.

Yöneticiler, yönetim panelinde (`/support/admin/statuses`) özel durumlar oluşturabilir ve yönetebilir.

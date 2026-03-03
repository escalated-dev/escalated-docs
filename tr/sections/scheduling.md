# Zamanlama

Escalated, otomatik bilet yaşam döngüsü yönetimi için artisan komutları sağlar. Bunları zamanlayıcınıza ekleyin.

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

## Kullanılabilir komutlar

- `escalated:check-sla` -- Açık biletleri SLA politikalarına göre kontrol eder ve `SlaBreached` olaylarını gönderir
- `escalated:evaluate-escalations` -- Yükseltme kurallarını eşleşen biletlere uygular ve yapılandırılmış eylemleri yürütür
- `escalated:run-automations` -- Zaman tabanlı otomasyon kurallarını uygun biletlere uygular
- `escalated:close-resolved` -- Yapılandırılmış gün sayısı boyunca "resolved" durumunda olan biletleri kapatır
- `escalated:purge-activities` -- Yapılandırılmış saklama süresinden eski etkinlik günlüğü girişlerini siler
- `escalated:purge-expired` -- Saklama politikası ayarlarına göre biletleri, ekleri ve denetim günlüklerini temizler
- `escalated:poll-imap` -- Yapılandırılmış IMAP posta kutusunu gelen e-postalar için yoklar

# Yapılandırma

Escalated, makul varsayılan ayarlarla kutudan çıkar çıkmaz çalışır. Yapılandırma isteğe bağlıdır ancak özelleştirme için kullanılabilir.

> **Yapılandırma seçenekleri**
>
> - `routes.prefix` -- Tüm Escalated rotaları için URL ön eki (varsayılan: `support`)
> - `routes.middleware` -- Müşteri rotalarına uygulanan ara katman yazılımı (varsayılan: `['web', 'auth']`)
> - `user_model` -- Kullanıcı modeli sınıfı (varsayılan: `App\Models\User`)
> - `table_prefix` -- Veritabanı tabloları için ön ek (varsayılan: `escalated_`)
> - `tickets.allow_customer_close` -- Müşterilerin kendi biletlerini kapatıp kapatamayacağı (varsayılan: `true`)
> - `tickets.auto_close_resolved_after_days` -- Çözülmüş biletleri N gün sonra otomatik kapatma (varsayılan: `7`)
> - `sla.business_hours_only` -- SLA hedefleri için yalnızca çalışma saatlerini sayma (varsayılan: `false`)
> - `notifications.channels` -- Bildirim kanalları (varsayılan: `['mail', 'database']`)

## Yönetim ayarları ve modülleri

Son platform güncellemeleri şunlar için yapılandırma ve yönetim ekranları ekler:

- Koşullu görünürlük kurallarıyla özel alanlar
- Özel durumlar ve çalışma saatleri takvimleri
- Roller (RBAC), yetenek tabanlı yönlendirme ve temsilci kapasitesi
- Denetim günlüğü inceleme
- Otomasyonlar ve giden webhook'lar
- CSAT anket davranışı
- SSO ve iki faktörlü kimlik doğrulama
- Veri saklama politikaları ve temizleme davranışı
- E-posta kanalı ayarları
- Özel nesneler ve kayıtlar

## Varlıkları yayınlama

```bash
# Publish config file
$ php artisan vendor:publish --tag=escalated-config

# Publish email templates for customization
$ php artisan vendor:publish --tag=escalated-views

# Publish migrations (if you need to customize)
$ php artisan vendor:publish --tag=escalated-migrations
```

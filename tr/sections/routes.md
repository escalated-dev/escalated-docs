# Rotalar

Escalated, yapılandırılmış ön ek altında üç grup rota kaydeder (varsayılan: `/support`).

## Müşteri rotaları

| Yöntem | URL | Açıklama |
| ------ | --- | ----------- |
| GET | /support | Müşteri bilet listesi |
| GET | /support/create | Yeni bilet formu |
| POST | /support | Bilet oluştur |
| GET | /support/kb | Bilgi tabanı ana sayfası |
| GET | /support/kb/{slug} | Bilgi tabanı makalesi |
| POST | /support/kb/{slug}/feedback | Makale geri bildirimi |
| GET | /support/{reference} | Bilet detayı |
| POST | /support/{reference}/reply | Bilete yanıt |
| POST | /support/{reference}/close | Bileti kapat |
| POST | /support/{reference}/reopen | Bileti yeniden aç |
| POST | /support/{reference}/rate | Memnuniyet değerlendirmesi gönder |

## Temsilci rotaları

`escalated-agent` kapısı gerektirir.

| Yöntem | URL | Açıklama |
| ------ | --- | ----------- |
| GET | /support/agent | Temsilci gösterge paneli |
| GET | /support/agent/tickets | Bilet kuyruğu |
| GET | /support/agent/tickets/{reference} | Bilet detayı |
| POST | /support/agent/tickets/{reference}/reply | Genel yanıt |
| POST | /support/agent/tickets/{reference}/note | Dahili not |
| POST | /support/agent/tickets/{reference}/assign | Temsilci ata |
| POST | /support/agent/tickets/{reference}/status | Durumu değiştir |
| POST | /support/agent/tickets/{reference}/priority | Önceliği değiştir |
| POST | /support/agent/tickets/bulk | Toplu bilet işlemleri |
| POST | /support/agent/tickets/{reference}/follow | Takibi aç/kapat |
| POST | /support/agent/tickets/{reference}/macro | Makro uygula |
| POST | /support/agent/tickets/{reference}/presence | Bulunma durumu bildir |
| POST | /support/agent/tickets/{reference}/typing | Yazım durumu bildir |
| POST | /support/agent/tickets/{reference}/replies/{reply}/pin | Not sabitlemeyi aç/kapat |

## Yönetici rotaları

`escalated-admin` kapısı gerektirir. Yöneticiler tüm temsilci rotalarına ek olarak yönetim sayfalarına sahiptir.

| Yöntem | URL | Açıklama |
| ------ | --- | ----------- |
| GET | /support/admin/reports | Analitik gösterge paneli |
| GET | /support/admin/departments | Departman yönetimi |
| GET | /support/admin/sla-policies | SLA politika yönetimi |
| GET | /support/admin/escalation-rules | Yükseltme kuralı oluşturucu |
| GET | /support/admin/tags | Etiket yönetimi |
| GET | /support/admin/canned-responses | Hazır yanıt şablonları |
| GET | /support/admin/macros | Makro yönetimi |
| GET | /support/admin/custom-fields | Özel alanlar ve formlar |
| GET | /support/admin/statuses | Özel durumlar |
| GET | /support/admin/business-hours | Çalışma saatleri takvimleri |
| GET | /support/admin/roles | Temsilci rolleri ve izinleri |
| GET | /support/admin/audit-log | Denetim günlüğü |
| GET | /support/admin/skills | Yetenek yönetimi |
| GET | /support/admin/capacity | Temsilci kapasite kontrolleri |
| GET | /support/admin/automations | Zaman tabanlı otomasyonlar |
| GET | /support/admin/webhooks | Giden webhook'lar |
| GET | /support/admin/webhooks/{webhook}/deliveries | Webhook teslimat günlüğü |
| GET | /support/admin/kb-articles | Bilgi tabanı makaleleri |
| GET | /support/admin/kb-categories | Bilgi tabanı kategorileri |
| GET | /support/admin/reports/dashboard | Raporlar gösterge paneli |
| GET | /support/admin/reports/agents | Temsilci verimlilik raporu |
| GET | /support/admin/reports/sla | SLA başarı raporu |
| GET | /support/admin/reports/csat | CSAT raporu |
| GET | /support/admin/settings/csat | CSAT anket ayarları |
| GET | /support/admin/settings/sso | SSO ayarları |
| GET | /support/admin/settings/two-factor | İki faktörlü kimlik doğrulama ayarları |
| GET | /support/admin/settings/data-retention | Veri saklama ayarları |
| GET | /support/admin/settings/email | E-posta kanalı ayarları |
| GET | /support/admin/custom-objects | Özel nesneler |
| GET | /support/admin/custom-objects/{customObject}/records | Özel nesne kayıtları |
| GET | /support/admin/tickets/merge-search | Birleştirme hedefi ara |
| POST | /support/admin/tickets/{reference}/merge | Bileti hedefe birleştir |
| GET | /support/admin/tickets/{reference}/links | Bağlantılı biletleri listele |
| POST | /support/admin/tickets/{reference}/links | İlgili bileti bağla |
| DELETE | /support/admin/tickets/{reference}/links/{link} | İlgili bileti bağlantısını kaldır |
| GET | /support/admin/tickets/{reference}/side-conversations | Yan konuşma listesi |
| POST | /support/admin/tickets/{reference}/side-conversations | Yan konuşma başlat |
| POST | /support/admin/tickets/{reference}/side-conversations/{sideConversation}/reply | Yan konuşmada yanıtla |
| POST | /support/admin/tickets/{reference}/side-conversations/{sideConversation}/close | Yan konuşmayı kapat |
| POST | /support/admin/macros | Makro oluştur |
| PUT | /support/admin/macros/{macro} | Makro güncelle |
| DELETE | /support/admin/macros/{macro} | Makro sil |

## Misafir rotaları

Kimlik doğrulama gerekmez. Benzersiz belirteç ile erişilir.

| Yöntem | URL | Açıklama |
| ------ | --- | ----------- |
| GET | /support/guest/create | Misafir bilet formu |
| POST | /support/guest | Misafir bilet oluştur |
| GET | /support/guest/{token} | Misafir bileti görüntüle |
| POST | /support/guest/{token}/reply | Misafir biletine yanıt ver |
| POST | /support/guest/{token}/rate | Memnuniyet değerlendirmesi gönder |

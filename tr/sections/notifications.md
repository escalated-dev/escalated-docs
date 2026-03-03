# Bildirimler

Escalated, framework'ünüzün yerel bildirim sistemini kullanır. Yeni biletler, yanıtlar, atamalar, durum değişiklikleri ve SLA ihlalleri gibi önemli olaylar için e-posta ve veritabanı bildirimleri otomatik olarak gönderilir.

- Bilet atanan kişi yeni yanıtlarda bilgilendirilir
- Talep eden, temsilci yanıtları ve durum değişikliklerinde bilgilendirilir
- **Bilet takipçileri** atanan kişiyle aynı bildirimleri alır -- yanıtlar ve durum değişiklikleri
- SLA ihlal uyarıları atanan kişiye ve departman üyelerine gönderilir

Görünümleri yayınlayarak e-posta şablonlarını özelleştirin: `php artisan vendor:publish --tag=escalated-views`

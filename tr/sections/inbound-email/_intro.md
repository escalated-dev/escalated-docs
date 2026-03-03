# Gelen E-posta

Gelen e-postalardan doğrudan bilet oluşturun ve yanıtlayın. Escalated, **Mailgun**, **Postmark**, **AWS SES** webhook'larını ve yedek olarak **IMAP** yoklamayı destekler.

## Nasıl Çalışır

1. E-posta sağlayıcınız destek adresinize bir mesaj alır (örneğin, `support@yourapp.com`)
2. Sağlayıcı bunu webhook aracılığıyla uygulamanıza iletir (veya IMAP yoklama getirir)
3. Escalated yükü normalleştirir ve konu referansı (örneğin, `[ESC-00001]`) veya `In-Reply-To` başlıkları aracılığıyla dizi eşleşmesini kontrol eder
4. Eşleşen e-postalar yanıt ekler; eşleşmeyenler yeni bir bilet oluşturur (veya bilinmeyen göndericiler için misafir bilet)

## Yapılandırma

Gelen e-postayı etkinleştirin ve adaptörünüzü yönetim ayarlarında veya ortam değişkenleri aracılığıyla yapılandırın. Yönetim ayarları ortam/yapılandırma değerlerine göre öncelik alır.

## Webhook URL'leri

E-posta sağlayıcınızın gelen webhook'unu bu URL'lere yönlendirin. Bu rotalar kimlik doğrulama gerektirmez (bunun yerine imza doğrulama kullanırlar).

| Sağlayıcı | Webhook URL |
| --- | --- |
| Mailgun | `POST /support/inbound/mailgun` |
| Postmark | `POST /support/inbound/postmark` |
| AWS SES | `POST /support/inbound/ses` |

## IMAP Yoklama

Webhook desteği olmayan e-posta sağlayıcıları için IMAP yoklama komutunu bir takvimde kullanın.

## Özellikler

- **Dizi algılama** -- konu referansı ve In-Reply-To / References başlıkları aracılığıyla
- **Misafir biletleri** -- bilinmeyen göndericiler için otomatik türetilmiş görüntüleme adlarıyla
- **Otomatik yeniden açma** -- e-posta ile bir yanıt geldiğinde çözülmüş veya kapatılmış biletleri yeniden aç
- **Yineleme algılama** -- yinelenen işlemeyi önlemek için Message-ID başlıkları aracılığıyla
- **Ek işleme** -- yapılandırılabilir boyut ve sayı sınırlarıyla
- **Denetim günlüğü** -- hata ayıklama ve uyumluluk için her gelen e-posta kaydedilir
- **Yönetimden yapılandırılabilir** -- tüm ayarlar ortam/yapılandırma yedeğiyle yönetim panelinden yönetilebilir

## 1. Eklentiyi kurun

```bash
$ wp plugin install escalated --activate
```

## 2. Ayarları yapılandırın

Departmanları, SLA politikalarını, yükseltme kurallarını ve e-posta kanallarını yapılandırmak için wp-admin'de **Escalated -> Settings** bölümüne gidin.

## 3. Kısa kodları ekleyin

Müşterilere destek portalı sağlamak için herhangi bir sayfaya kısa kodlar yerleştirin:

```shortcodes
[escalated_tickets]        // Ticket list
[escalated_create_ticket]  // New ticket form
[escalated_view_ticket]    // Ticket detail
```

> **Not:** WordPress eklentisi bağımsızdır -- Inertia.js kullanmaz. Tüm arayüz yerel WordPress yönetim ekranları ve kısa kod destekli ön yüz şablonları aracılığıyla oluşturulur.

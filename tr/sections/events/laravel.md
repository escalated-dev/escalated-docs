```php
use Escalated\Laravel\Events\TicketCreated;

Event::listen(TicketCreated::class, function ($event) {
    // $event->ticket
});
```

**Kullanılabilir olaylar**

- `TicketCreated` -- Yeni bilet gönderildi
- `TicketStatusChanged` -- Durum geçişi
- `TicketPriorityChanged` -- Öncelik güncellendi
- `TicketAssigned` -- Bilete temsilci atandı
- `TicketUnassigned` -- Temsilci biletten kaldırıldı
- `ReplyCreated` -- Genel yanıt eklendi
- `InternalNoteAdded` -- Temsilci dahili notu
- `TicketUpdated` -- Bilet meta verileri değiştirildi
- `TicketReopened` -- Bilet aktif duruma geri döndü
- `DepartmentChanged` -- Departman yeniden atandı
- `TagAddedToTicket` -- Bilete etiket uygulandı
- `TagRemovedFromTicket` -- Biletten etiket kaldırıldı
- `SlaWarning` -- Bilet SLA son tarihine yaklaşıyor
- `SlaBreached` -- SLA son tarihi kaçırıldı
- `TicketEscalated` -- Bilet kural tarafından yükseltildi
- `TicketResolved` -- Bilet çözülmüş olarak işaretlendi
- `TicketClosed` -- Bilet kapatıldı

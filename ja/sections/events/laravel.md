```php
use Escalated\Laravel\Events\TicketCreated;

Event::listen(TicketCreated::class, function ($event) {
    // $event->ticket
});
```

**利用可能なイベント**

- `TicketCreated` -- 新しいチケットが送信された
- `TicketStatusChanged` -- ステータスが遷移した
- `TicketPriorityChanged` -- 優先度が更新された
- `TicketAssigned` -- エージェントがチケットに割り当てられた
- `TicketUnassigned` -- エージェントがチケットから外された
- `ReplyCreated` -- 公開返信が追加された
- `InternalNoteAdded` -- エージェントの内部メモ
- `TicketUpdated` -- チケットのメタデータが変更された
- `TicketReopened` -- チケットがアクティブ状態に戻された
- `DepartmentChanged` -- 部門が再割り当てされた
- `TagAddedToTicket` -- チケットにタグが適用された
- `TagRemovedFromTicket` -- チケットからタグが削除された
- `SlaWarning` -- チケットがSLA期限に近づいている
- `SlaBreached` -- SLA期限を超過した
- `TicketEscalated` -- ルールによりチケットがエスカレートされた
- `TicketResolved` -- チケットが解決済みになった
- `TicketClosed` -- チケットがクローズされた

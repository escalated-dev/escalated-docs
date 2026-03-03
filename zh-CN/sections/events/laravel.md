```php
use Escalated\Laravel\Events\TicketCreated;

Event::listen(TicketCreated::class, function ($event) {
    // $event->ticket
});
```

**可用事件**

- `TicketCreated` -- 新工单已提交
- `TicketStatusChanged` -- 状态转换
- `TicketPriorityChanged` -- 优先级更新
- `TicketAssigned` -- 客服被分配到工单
- `TicketUnassigned` -- 客服从工单中移除
- `ReplyCreated` -- 添加了公开回复
- `InternalNoteAdded` -- 客服内部备注
- `TicketUpdated` -- 工单元数据已更改
- `TicketReopened` -- 工单已恢复为活跃状态
- `DepartmentChanged` -- 部门已重新分配
- `TagAddedToTicket` -- 标签已应用到工单
- `TagRemovedFromTicket` -- 标签已从工单移除
- `SlaWarning` -- 工单接近SLA截止时间
- `SlaBreached` -- SLA截止时间已超过
- `TicketEscalated` -- 工单被规则升级
- `TicketResolved` -- 工单被标记为已解决
- `TicketClosed` -- 工单已关闭

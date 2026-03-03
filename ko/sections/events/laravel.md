```php
use Escalated\Laravel\Events\TicketCreated;

Event::listen(TicketCreated::class, function ($event) {
    // $event->ticket
});
```

**사용 가능한 이벤트**

- `TicketCreated` -- 새 티켓이 제출됨
- `TicketStatusChanged` -- 상태 전환
- `TicketPriorityChanged` -- 우선순위 업데이트
- `TicketAssigned` -- 에이전트가 티켓에 할당됨
- `TicketUnassigned` -- 에이전트가 티켓에서 해제됨
- `ReplyCreated` -- 공개 답변 추가
- `InternalNoteAdded` -- 에이전트 내부 메모
- `TicketUpdated` -- 티켓 메타데이터 변경
- `TicketReopened` -- 티켓이 활성 상태로 복원됨
- `DepartmentChanged` -- 부서 재할당
- `TagAddedToTicket` -- 티켓에 태그 적용
- `TagRemovedFromTicket` -- 티켓에서 태그 제거
- `SlaWarning` -- 티켓이 SLA 마감에 근접
- `SlaBreached` -- SLA 마감 초과
- `TicketEscalated` -- 규칙에 의해 티켓이 에스컬레이션됨
- `TicketResolved` -- 티켓이 해결됨으로 표시됨
- `TicketClosed` -- 티켓이 종료됨

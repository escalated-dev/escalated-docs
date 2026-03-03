```php
use Escalated\Laravel\Contracts\HasTickets;
use Escalated\Laravel\Contracts\Ticketable;

class User extends Authenticatable implements Ticketable
{
    use HasFactory, HasTickets, Notifiable;
}
```

`HasTickets` 트레이트는 사용자 모델에 `tickets()` 관계 및 헬퍼 메서드를 제공합니다.

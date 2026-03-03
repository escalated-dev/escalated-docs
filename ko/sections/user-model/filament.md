```php
use Escalated\Laravel\Contracts\HasTickets;
use Escalated\Laravel\Contracts\Ticketable;

class User extends Authenticatable implements Ticketable
{
    use HasFactory, HasTickets, Notifiable;
}
```

Filament는 `escalated-laravel` 패키지의 래퍼이므로 동일한 사용자 모델 설정을 사용합니다.

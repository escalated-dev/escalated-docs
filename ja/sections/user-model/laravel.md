```php
use Escalated\Laravel\Contracts\HasTickets;
use Escalated\Laravel\Contracts\Ticketable;

class User extends Authenticatable implements Ticketable
{
    use HasFactory, HasTickets, Notifiable;
}
```

`HasTickets`トレイトはユーザーモデルに`tickets()`リレーションとヘルパーメソッドを提供します。

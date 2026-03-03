```php
use Escalated\Laravel\Contracts\HasTickets;
use Escalated\Laravel\Contracts\Ticketable;

class User extends Authenticatable implements Ticketable
{
    use HasFactory, HasTickets, Notifiable;
}
```

Трейт `HasTickets` предоставляет связь `tickets()` и вспомогательные методы для модели пользователя.

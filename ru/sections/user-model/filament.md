```php
use Escalated\Laravel\Contracts\HasTickets;
use Escalated\Laravel\Contracts\Ticketable;

class User extends Authenticatable implements Ticketable
{
    use HasFactory, HasTickets, Notifiable;
}
```

Filament использует ту же настройку модели пользователя из `escalated-laravel`, так как является обёрткой над пакетом Laravel.

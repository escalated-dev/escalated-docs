```php
use Escalated\Laravel\Contracts\HasTickets;
use Escalated\Laravel\Contracts\Ticketable;

class User extends Authenticatable implements Ticketable
{
    use HasFactory, HasTickets, Notifiable;
}
```

Filament korzysta z tej samej konfiguracji modelu użytkownika `escalated-laravel`, ponieważ jest opakowaniem pakietu Laravel.

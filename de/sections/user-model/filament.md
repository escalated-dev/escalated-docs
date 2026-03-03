```php
use Escalated\Laravel\Contracts\HasTickets;
use Escalated\Laravel\Contracts\Ticketable;

class User extends Authenticatable implements Ticketable
{
    use HasFactory, HasTickets, Notifiable;
}
```

Filament verwendet dasselbe `escalated-laravel` User-Model-Setup, da es ein Laravel-Paket-Wrapper ist.

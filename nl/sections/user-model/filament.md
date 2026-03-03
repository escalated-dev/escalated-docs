```php
use Escalated\Laravel\Contracts\HasTickets;
use Escalated\Laravel\Contracts\Ticketable;

class User extends Authenticatable implements Ticketable
{
    use HasFactory, HasTickets, Notifiable;
}
```

Filament gebruikt dezelfde gebruikersmodelconfiguratie van `escalated-laravel`, aangezien het een Laravel-pakketwrapper is.

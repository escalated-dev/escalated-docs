```php
use Escalated\Laravel\Contracts\HasTickets;
use Escalated\Laravel\Contracts\Ticketable;

class User extends Authenticatable implements Ticketable
{
    use HasFactory, HasTickets, Notifiable;
}
```

De `HasTickets`-trait biedt een `tickets()`-relatie en hulpmethoden op het gebruikersmodel.

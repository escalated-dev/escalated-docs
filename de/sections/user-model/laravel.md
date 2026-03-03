```php
use Escalated\Laravel\Contracts\HasTickets;
use Escalated\Laravel\Contracts\Ticketable;

class User extends Authenticatable implements Ticketable
{
    use HasFactory, HasTickets, Notifiable;
}
```

Der `HasTickets`-Trait stellt eine `tickets()`-Beziehung und Hilfsmethoden für das User Model bereit.

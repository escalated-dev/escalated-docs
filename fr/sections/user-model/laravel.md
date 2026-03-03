```php
use Escalated\Laravel\Contracts\HasTickets;
use Escalated\Laravel\Contracts\Ticketable;

class User extends Authenticatable implements Ticketable
{
    use HasFactory, HasTickets, Notifiable;
}
```

Le trait `HasTickets` fournit une relation `tickets()` et des methodes auxiliaires sur le modele utilisateur.

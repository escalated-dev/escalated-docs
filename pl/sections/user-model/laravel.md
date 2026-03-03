```php
use Escalated\Laravel\Contracts\HasTickets;
use Escalated\Laravel\Contracts\Ticketable;

class User extends Authenticatable implements Ticketable
{
    use HasFactory, HasTickets, Notifiable;
}
```

Trait `HasTickets` udostępnia relację `tickets()` oraz metody pomocnicze na modelu użytkownika.

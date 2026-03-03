```php
use Escalated\Laravel\Contracts\HasTickets;
use Escalated\Laravel\Contracts\Ticketable;

class User extends Authenticatable implements Ticketable
{
    use HasFactory, HasTickets, Notifiable;
}
```

El trait `HasTickets` proporciona una relacion `tickets()` y metodos auxiliares en el modelo de usuario.

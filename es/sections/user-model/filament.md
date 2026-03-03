```php
use Escalated\Laravel\Contracts\HasTickets;
use Escalated\Laravel\Contracts\Ticketable;

class User extends Authenticatable implements Ticketable
{
    use HasFactory, HasTickets, Notifiable;
}
```

Filament utiliza la misma configuracion de modelo de usuario de `escalated-laravel` ya que es un wrapper del paquete Laravel.

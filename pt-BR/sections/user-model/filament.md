```php
use Escalated\Laravel\Contracts\HasTickets;
use Escalated\Laravel\Contracts\Ticketable;

class User extends Authenticatable implements Ticketable
{
    use HasFactory, HasTickets, Notifiable;
}
```

O Filament utiliza a mesma configuracao de modelo de usuario do `escalated-laravel`, pois e um wrapper de pacote Laravel.

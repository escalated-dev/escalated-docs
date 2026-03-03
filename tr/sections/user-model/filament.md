```php
use Escalated\Laravel\Contracts\HasTickets;
use Escalated\Laravel\Contracts\Ticketable;

class User extends Authenticatable implements Ticketable
{
    use HasFactory, HasTickets, Notifiable;
}
```

Filament, bir Laravel paket sarmalayıcısı olduğu için `escalated-laravel` ile aynı kullanıcı modeli kurulumunu kullanır.

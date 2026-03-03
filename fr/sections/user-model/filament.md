```php
use Escalated\Laravel\Contracts\HasTickets;
use Escalated\Laravel\Contracts\Ticketable;

class User extends Authenticatable implements Ticketable
{
    use HasFactory, HasTickets, Notifiable;
}
```

Filament utilise la meme configuration de modele utilisateur que `escalated-laravel` puisqu'il s'agit d'un wrapper du package Laravel.

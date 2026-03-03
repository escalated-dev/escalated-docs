```php
use Escalated\Laravel\Contracts\HasTickets;
use Escalated\Laravel\Contracts\Ticketable;

class User extends Authenticatable implements Ticketable
{
    use HasFactory, HasTickets, Notifiable;
}
```

Filament utilizza la stessa configurazione del modello utente di `escalated-laravel` poiché è un wrapper del pacchetto Laravel.

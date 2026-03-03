```php
use Escalated\Laravel\Contracts\HasTickets;
use Escalated\Laravel\Contracts\Ticketable;

class User extends Authenticatable implements Ticketable
{
    use HasFactory, HasTickets, Notifiable;
}
```

`HasTickets` trait'i, kullanıcı modelinde `tickets()` ilişkisini ve yardımcı metotları sağlar.

```php
use Escalated\Laravel\Contracts\HasTickets;
use Escalated\Laravel\Contracts\Ticketable;

class User extends Authenticatable implements Ticketable
{
    use HasFactory, HasTickets, Notifiable;
}
```

توفر سمة `HasTickets` علاقة `tickets()` وطرق مساعدة على نموذج المستخدم.

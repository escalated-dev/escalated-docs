```php
use Escalated\Laravel\Contracts\HasTickets;
use Escalated\Laravel\Contracts\Ticketable;

class User extends Authenticatable implements Ticketable
{
    use HasFactory, HasTickets, Notifiable;
}
```

يستخدم Filament نفس إعداد نموذج المستخدم في `escalated-laravel` لأنه مغلف لحزمة Laravel.

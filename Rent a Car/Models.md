Beispiel:
```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Foundation\Auth\User as Authenticatable;
use Illuminate\Notifications\Notifiable;

class User extends Authenticatable
{
    use HasFactory, Notifiable;

    protected $table = 'user';
    
    protected $fillable = ['name', 'active', 'birthday'];

    protected function casts(): array
    {
        return [
            'active'   => 'boolean',
            'birthday' => 'date',
        ];
    }
}

```
`$table` gibt den Namen der Tabelle an.
`$fillable` gibt an welche Attribute mit Arrays gefühlt werden können im Seeder.
`casts()` gibt an wie Werte konvertiert werden beim GET/SET. (wird für Funktionen im Seeder wie z.B. firstOrCreate verwendet.)
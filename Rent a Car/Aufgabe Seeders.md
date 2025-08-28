Es muss für jede Tabelle/Migration auch ein Modell (App/Models/) erstellt werden.
[[Models]]

Code DatabaseSeeders.php
```php
<?php

namespace Database\Seeders;

use App\Models\User;
use Illuminate\Database\Seeder;

class DatabaseSeeder extends Seeder
{
    public function run(): void
    {
        User::firstOrCreate(
            ['name' => 'admin'],
            [
                'active'   => true,
                'birthday' => null,
            ]
        );
    }
}
```

Adjustment User Model "User.php"
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


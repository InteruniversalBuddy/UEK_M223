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

# Erstellte Models
---
## Car.php
```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Foundation\Auth\User as Authenticatable;
use Illuminate\Notifications\Notifiable;
use Illuminate\Database\Eloquent\Relations\HasMany;

class Car extends Authenticatable
{
    use HasFactory, Notifiable;

    protected $table = 'car';

    /**
     * Mass assignable attributes.
     *
     * @var list<string>
     */
    protected $fillable = ['brand', 'color'];

    /**
     * Attribute casts.
     *
     * @return array<string, string>
     */
    protected function casts(): array
    {
        return [
            'active'   => 'boolean'
        ];
    }

    // Optional: relationships (if you created them)
    // public function reservations()
    // {
    //     return $this->hasMany(Reservation::class);
    // }

    public function reservations(): HasMany
    {
        return $this->hasMany(Reservation::class);
    }
}
```
## User.php
```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Foundation\Auth\User as Authenticatable;
use Illuminate\Notifications\Notifiable;
use Illuminate\Database\Eloquent\Relations\HasMany;

class User extends Authenticatable
{
    use HasFactory, Notifiable;

    protected $table = 'user';

    /**
     * Mass assignable attributes.
     *
     * @var list<string>
     */
    protected $fillable = ['name', 'active', 'birthday'];

    /**
     * Attribute casts.
     *
     * @return array<string, string>
     */
    protected function casts(): array
    {
        return [
            'active'   => 'boolean',
            'birthday' => 'date'
        ];
    }

    // Optional: relationships (if you created them)
    // public function reservations()
    // {
    //     return $this->hasMany(Reservation::class);
    // }
    public function reservations(): HasMany
    {
        return $this->hasMany(\App\Models\Reservation::class);
    }
}
```
## Reservation.php
```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Foundation\Auth\User as Authenticatable;
use Illuminate\Notifications\Notifiable;
use Illuminate\Database\Eloquent\Relations\BelongsTo;

class Reservation extends Authenticatable
{
    use HasFactory, Notifiable;

    protected $table = 'reservation';

    /**
     * Mass assignable attributes.
     *
     * @var list<string>
     */
    protected $fillable = ['dateStart','dateEnd'];

    /**
     * Attribute casts.
     *
     * @return array<string, string>
     */
    protected function casts(): array
    {
        return [
            'active'   => 'boolean'
        ];
    }

    // Optional: relationships (if you created them)
    // public function reservations()
    // {
    //     return $this->hasMany(Reservation::class);
    // }


    public function car(): BelongsTo
    {
        return $this->belongsTo(Car::class);   // uses car_id
    }

    public function user(): BelongsTo
    {
        return $this->belongsTo(User::class);  // uses user_id
    }
}
```

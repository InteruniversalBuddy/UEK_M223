Command um die Factory für ein Model zu erstellen (nur Struktur):
```php
ddev php artisan make:factory NameFactory --model=Model
```

Beispiel Code:
```php
// Beispiel für Reservation
<?php

namespace Database\Factories;

use Illuminate\Database\Eloquent\Factories\Factory;
use Illuminate\Support\Facades\Hash;
use Illuminate\Support\Str;

use App\Models\User;
use App\Models\Car;

class ReservationFactory extends Factory
{
    public function definition(): array
    {
        return [
            'user_id' => User::factory(),
            'car_id' => Car::factory(),
            'date_start' => fake()->date(),
            'date_end' => fake()->date()
        ];
    }

}


```

`fake()` erstellt einen Beispiel Attribut von dem danach angegebenen Typ.
Um Fremdschlüssel anzugeben, die andere Factory auswählen `(z.B. User::factory()`)

seedeers/RolePermissionSeeder.php
File erstellen
```php
<?php

namespace Database\Seeders;

use Illuminate\Database\Seeder;
use Spatie\Permission\Models\Role;
use Spatie\Permission\Models\Permission;

class RolePermissionSeeder extends Seeder
{
    public function run(): void
    {
        // Abteilungen (Rollen) erstellen
        Role::firstOrCreate(['name' => 'admin']);
        Role::firstOrCreate(['name' => 'sales']);
        Role::firstOrCreate(['name' => 'service']);

        // Berechtigungen erstellen
        Permission::firstOrCreate(['name' => 'edit cars']);
        Permission::firstOrCreate(['name' => 'delete rentals']);
        Permission::firstOrCreate(['name' => 'view customers']);
        Permission::firstOrCreate(['name' => 'create service entries']);
        Permission::firstOrCreate(['name' => 'view cars']); // wird weiter unten verwendet
    
      // Rollen
    $admin   = Role::firstOrCreate(['name' => 'admin']);
    $sales   = Role::firstOrCreate(['name' => 'sales']);
    $service = Role::firstOrCreate(['name' => 'service']);

    // Berechtigungen
    $editCars     = Permission::firstOrCreate(['name' => 'edit cars']);
    $deleteRent   = Permission::firstOrCreate(['name' => 'delete rentals']);
    $viewCustomers= Permission::firstOrCreate(['name' => 'view customers']);
    $createService= Permission::firstOrCreate(['name' => 'create service entries']);
    $viewCars     = Permission::firstOrCreate(['name' => 'view cars']);

    // Berechtigungen Rollen zuweisen
    $sales->givePermissionTo([$editCars, $deleteRent]);
    $service->givePermissionTo([$viewCars, $createService]);
    $admin->givePermissionTo(Permission::all()); // Admin bekommt alles
    
    }
}
```
seeders/DatabaseSeeder.php 

Code hinzufügen
```php
    use Spatie\Permission\Models\Role;
```

```php
          $this->call(RolePermissionSeeder::class);
            // Rollen aus DB holen
            $adminRole   = Role::where('name', 'admin')->first();
            $salesRole   = Role::where('name', 'sales')->first();
            $serviceRole = Role::where('name', 'service')->first();
            // User mit Rollen verknüpfen
            $admin->assignRole($adminRole);
            $seller->assignRole($salesRole);
            $service->assignRole($serviceRole);
    
```


bootstrap/app.php
```php
<?php

use Illuminate\Foundation\Application;
use Illuminate\Foundation\Configuration\Exceptions;
use Illuminate\Foundation\Configuration\Middleware;
use Spatie\Permission\Middleware\RoleMiddleware;
use Spatie\Permission\Middleware\PermissionMiddleware;
use Spatie\Permission\Middleware\RoleOrPermissionMiddleware;

return Application::configure(basePath: dirname(__DIR__))
    ->withRouting(
        web: __DIR__.'/../routes/web.php',
        commands: __DIR__.'/../routes/console.php',
        health: '/up',
    )
    ->withMiddleware(function (Middleware $middleware) {
        $middleware->alias([
            'role'               => RoleMiddleware::class,
            'permission'         => PermissionMiddleware::class,
            'role_or_permission' => RoleOrPermissionMiddleware::class,
        ]);
    })
    ->withExceptions(function (Exceptions $exceptions): void {
        //
    })
    ->create();
```

routes/web.php
```php
Route::group(['middleware' => ['auth']], function() {
    Route::resource('roles', RoleController::class);
    Route::resource('users', UserController::class);
});
```

Falls **App\Http\Controllers\CarsController.php** noch nicht exsestiert
```bash
ddev php artisan make:controller CarsController --resource
```

CarsController.php
``` php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

class CarsController extends Controller
{
    /**
     * Display a listing of the resource.
     */
    public function index()
    {
        //
    }

    /**
     * Show the form for creating a new resource.
     */
    public function create()
    {
        //
    }

    /**
     * Store a newly created resource in storage.
     */
    public function store(Request $request)
    {
        //
    }

    /**
     * Display the specified resource.
     */
    public function show(string $id)
    {
        //
    }

    /**
     * Show the form for editing the specified resource.
     */
    public function edit(string $id)
    {
        //
    }

    /**
     * Update the specified resource in storage.
     */
    public function update(Request $request, string $id)
    {
        //
    }

    /**
     * Remove the specified resource from storage.
     */
    public function destroy(string $id)
    {
        //
    }
}
```
## routes/web.php

``` php
use App\Http\Controllers\CarsController;
```

```php
Route::middleware(['auth'])->group(function () {
    Route::resource('cars', CarsController::class);
});
```
## App/Http/Controllers/Controller.php
```php
<?php

namespace App\Http\Controllers;

use Illuminate\Foundation\Auth\Access\AuthorizesRequests;
use Illuminate\Foundation\Validation\ValidatesRequests;
use Illuminate\Routing\Controller as BaseController;

class Controller extends BaseController
{
    use AuthorizesRequests, ValidatesRequests;
}
```

Models/User.php
```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Foundation\Auth\User as Authenticatable;
use Illuminate\Notifications\Notifiable;
use Illuminate\Database\Eloquent\Relations\HasMany;
use Spatie\Permission\Traits\HasRoles;

// Filament
use Filament\Models\Contracts\FilamentUser;
use Filament\Panel;

class User extends Authenticatable implements FilamentUser
{
    use HasFactory, Notifiable, HasRoles;

    protected $table = 'user'; // wir nutzen singuläre Tabellennamen

    protected $fillable = ['name', 'email', 'password', 'active', 'birthday'];

    protected $hidden = ['password', 'remember_token'];

    protected function casts(): array
    {
        return [
            'active'            => 'boolean',
            'birthday'          => 'date',
            'email_verified_at' => 'datetime',
        ];
    }

    public function reservations(): HasMany
    {
        return $this->hasMany(\App\Models\Reservation::class, 'user_id');
    }

    /**
     * Nur bestimmte User dürfen das Filament-Panel (/admin) betreten.
     */
    public function canAccessPanel(Panel $panel): bool
    {
        // Variante A: Nur Rolle "admin"
        return $this->hasRole('admin');

        // Variante B (falls du eine Permission "access admin panel" im Seeder erstellt hast):
        // return $this->hasPermissionTo('access admin panel');
    }
}
```

## Cache reseten
```
ddev php artisan optimize:clear
ddev php artisan permission:cache-reset
```

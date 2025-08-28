### Filament installieren 
```bash
# Filament installieren (neueste Version)
ddev composer require filament/filament -W

# Filament mit Panels installieren
ddev php artisan filament:install --panels

# Optimierungen (Cache aufbauen/leeren)
ddev php artisan filament:optimize
ddev php artisan filament:optimize-clear
```
Um den admin User zu erstellen im Seeder:
```
User::factory()->create([
    'name' => 'admin',
    'email' => 'admin@example.com',
    'password' => bcrypt('admin')
]);
```

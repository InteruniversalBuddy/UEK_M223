Beispiel Codes:
- Nur Tabelle einzeigen
```php
Route::get('/car-json', fn() => \App\Models\Car::limit(10)->get());
```
- Mit Fremdschlüssel
```php
Route::get('/reservation-json', fn() => \App\Models\Reservation::with(['car','user'])->limit(10)->get());
```
`limit()` Setzt ein Limit für die Anzahl geladenen Datensätze.

https://lernen.zbw.ch/mod/page/view.php?id=74893

---
## 1. Datenbank
- [ ] Migration erstellen (php artisan make:migration create_xyz_table)
- [ ] Spalten definieren (z. B. name, description, timestamps)
- [ ] Migration ausführen (php artisan migrate)
- [ ] Seeder erstellen und Testdaten einfügen (php artisan db:seed)
- [ ] Testen (ist die DB auch in DBeaver vorhanden?)
## 2. Modell
- [ ] Eloquent Model erstellen (php artisan make:model Xyz)
- [ ] Beziehungen definieren (belongsTo, hasMany, etc.)
- [ ] $fillable oder $guarded Felder festlegen
## 3. Filament Resource
- [ ] Neue Resource erstellen (php artisan make:filament-resource Xyz)
- [ ] Formulare (Schemas/XyzForm.php) anpassen
- [ ] Tabellen (Tables/XyzTable.php) konfigurieren
- [ ] Detailansicht (Schemas/XyzInfolist.php) einrichten
- [ ] Seiten (Pages/) prüfen: Create, Edit, List, View
## 4. Berechtigungen
- [ ] Spatie Permission installieren & konfigurieren (falls nicht vorhanden)
- [ ] Neue Rollen & Berechtigungen für xyz definieren
- [ ] Trait HasCrudPermissions ins Resource einbinden
- [ ] Policy erstellen (php artisan make:policy XyzPolicy)
- [ ] Testen (sind in der DB auch die richtigen Daten vorhanden?)
## 5. Logging
- [ ] Änderungen im Observer oder Event loggen
- [ ] Optional: Activity Log (spatie/laravel-activitylog) integrieren
- [ ] Wichtige Aktionen (create, update, delete) protokollieren
- [ ] Testen (sind in der DB auch die richtigen Daten vorhanden?)
## 6. Tests mit PHPUnit
- [ ] Feature-Test für CRUD schreiben
- [ ] Auth & Permission Tests einfügen
- [ ] Datenbank-Seed Tests prüfen

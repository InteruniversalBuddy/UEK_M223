https://lernen.zbw.ch/mod/assign/view.php?id=73061
[[Add delete button]]

---
### Table
**Fügt Delete Button in Tabellen Ansicht hinzu**

Im CarsTable.php bei `->actions()` die `DeleteAction::make()` hinzufügen.
Der use Pfad dafür muss auch hinzugefügt werden `use Filament\Actions\DeleteAction;`.
### Edit Car
**Fügt Delete Button in Bearbeitungs-Ansicht hinzu**

Im EditCar.php das use `use Filament\Actions\DeleteAction;` und diesen Block hinzufügen:
```php
protected function getHeaderActions(): array
{
    return [
        DeleteAction::make(),
    ];
}
```

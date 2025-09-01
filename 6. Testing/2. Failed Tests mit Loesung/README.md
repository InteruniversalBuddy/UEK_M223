Testen:
```bash
ddev php artisan optimize:clear
ddev php artisan migrate:fresh
ddev php artisan migrate:refresh --seed
ddev php artisan test
```

Mit dem Resultat in einer Text-Datei:
```bash
ddev php artisan optimize:clear
ddev php artisan migrate:fresh
ddev php artisan migrate:refresh --seed
ddev php artisan test > test.txt
```

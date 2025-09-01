# Problem
---
Nach dem Registrieren wird ein error mit "default value" hingegeben.
![[Pasted image 20250901104842.png]]
# Lösung
---
Beim Model von "User.php" die Werte mit dem Error in die `$fillable` Variable hinzufügen:
```php
    protected $fillable = ['name', 'active', 'birthday', 'email', 'password'];
```

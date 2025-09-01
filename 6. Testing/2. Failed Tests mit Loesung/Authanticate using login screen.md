# Problem
---
```
Okay lets do it one by one, how do I solve this one:
   FAIL  Tests\Feature\Auth\AuthenticationTest
  ✓ login screen can be rendered                                                                                                                                                                                                                   0.56s  
  ⨯ users can authenticate using the login screen                                                                                                                                                                                                  0.51s  
  ✓ users can not authenticate with invalid password                                                                                                                                                                                               0.33s  
  ✓ users can logout                                                                                                                                                                                                                               0.03s
```
# Lösung
---
## Bycrypt hash für Passwort
Bei "UserFactory.php" `return[]` so anpassen:
```php
            'name' => fake()->name(),
            'email' => fake()->unique()->safeEmail(),
            'email_verified_at' => now(),
            'password' => '$2y$10$92IXUNpkjO0rOQ5byMi.Ye4oKoEa3Ro9llC/.og/at2.uheWG/igi',
            'remember_token' => Str::random(10),
```
## User Model: Mass Assignement
Beim `casts()` von "User.php" das **Hinzufügen**:
```php
            'email_verified_at' => 'datetime',
            'password' => 'hashed',
```

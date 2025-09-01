In "User.php" in `casts` **auskommentiert**
```php
            // remove: 'password' => 'hashed',
```

In "UserFactory.php" die `unverified()` Funktion hinzufügen:
```php
    public function unverified(): static
    {
        return $this->state(fn () => [
            'email_verified_at' => null,
        ]);
    }
```

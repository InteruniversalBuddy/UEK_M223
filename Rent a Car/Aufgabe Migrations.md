```php
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

return new class extends Migration
{
    /**
     * Run the migrations.
     */
    public function up(): void
    {
        // USERS
        Schema::create('user', function (Blueprint $table) {
            $table->id();                                   // big integer pk
            $table->boolean('active')->default(true);
            $table->string('name');
            $table->date('birthday')->nullable();
            $table->timestamps();
        });

        // CARS
        Schema::create('car', function (Blueprint $table) {
            $table->id();                                   // big integer pk
            $table->boolean('active')->default(true);
            $table->string('brand');
            $table->string('color');
            $table->timestamps();
        });

        // RESERVATIONS (Laravel-style FKs)
        Schema::create('reservation', function (Blueprint $table) {
            $table->id();                                   // big integer pk
            $table->boolean('active')->default(true);
            $table->date('date_start')->nullable();
            $table->date('date_end')->nullable();

            $table->foreignId('car_id')
                ->constrained('car')
                ->cascadeOnDelete();

            $table->foreignId('user_id')
                ->constrained('user')
                ->cascadeOnDelete();

            $table->timestamps();
        });

        // SESSIONS (official Laravel layout)
        Schema::create('sessions', function (Blueprint $table) {
            $table->string('id')->primary();
            $table->foreignId('user_id')->nullable()->index(); // no FK constraint by default
            $table->string('ip_address', 45)->nullable();
            $table->text('user_agent')->nullable();
            $table->longText('payload');
            $table->integer('last_activity')->index();
        });
    }

    /**
     * Reverse the migrations.
     */
    public function down(): void
    {
        // Drop in FK-safe order
        Schema::disableForeignKeyConstraints();

        Schema::dropIfExists('sessions');
        Schema::dropIfExists('reservation');
        Schema::dropIfExists('car');
        Schema::dropIfExists('user');

        Schema::enableForeignKeyConstraints();
    }
};

```

Migrationen neu ausführen:
```
ddev php artisan migrate:fresh
```
Um zu sehen was schon erstellt wurde:
```
ddev php artisan migrate:status
```

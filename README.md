## This is Laravel Starter Kit
Functions
- include Spatie Laravel permission with route/web.php and PermisisonsSeeder.php(sample)
- Separete Admin, Frontend Directory  Controller, view.

### Setup
~~~
$ git clone https://github.com/boltnut2020/laravel-admin-starter.git
$ cd laravel-admin-starter
$ composer install
$ cp .env.example .env
$ mysql -uroot -p
mysql> create database laravel;
$ php artisan key:generate
$ php artisan migrate --seed
$ php artisan serve
~~~
Open browser "http://127.0.0.1:8000/"
Try Login "admin@example.com:password"

Change Admin Password & migration refresh.
~~~
in database/seeds/PermissionsSeeder.php

24         $user = Factory(App\User::class)->create([
25             'name' => 'Admin',
26             'email' => 'admin@example.com',
27             'password' => Hash::make('password'), // Change this "password" to your secret password.
28         ]);
~~~

Reset your seeder.
~~~
$ php artisan migrate:fresh --seed --seeder=PermissionsSeeder
~~~

### Features
~~~
Separete Frontend,Admin

$ tree -L 1 app/Http/Controllers/
app/Http/Controllers/
├── Admin
├── Auth
├── Controller.php
└── Frontend

$ tree -L 1 resources/views
resources/views
├── admin
└── frontend

Set Spatie Laravel Permission on route base.

$ vi routes/web.php
 17 Auth::routes();
 18
 19 // User who has admin role can access.
 20 Route::group(['prefix' => 'admin', 'as' => 'admin.', 'namespace' => 'Admin', 'middleware' => ['role:admin']], function () {
 21 });
 22
 23 // User who has admin|member role can access.
 24 Route::group(['prefix' => 'admin', 'as' => 'admin.', 'namespace' => 'Admin', 'middleware' => ['role:admin|member|guest']], function () {
 25     Route::get('home', 'HomeController@index')->name('home');
 26 });
~~~

# Entrance
Full entrance package, including login and password reset.

## Install
```bash
composer require intothesource/entrance
```

## After install

#### ServiceProvider
Add the following line to "config/app.php"

at "providers":

```bash
IntoTheSource\Entrance\EntranceServiceProvider::class,
Illuminate\Html\HtmlServiceProvider::class,
```

And at "aliases":

```bash
'Form'      => Illuminate\Html\FormFacade::class,
'HTML'      => Illuminate\Html\HtmlFacade::class,
```

#### Creating the files
Run the following command:

```bash
php artisan vendor:publish
```

#### Migration

Run the command: 
```bash
php artisan migrate
```

#### Middleware

Add the following lines to the '$routeMiddleware' array in the file 'App/Http/Kernel.php'

```bash
'checktoken' => \IntoTheSource\Entrance\Http\Middleware\CheckToken::class,
'checklogin' => \IntoTheSource\Entrance\Http\Middleware\CheckLogin::class,
```

#### E-Mails
This package sends e-mails. Be sure to configure your mail settings.
Set the global FROM adres inside -> config/mail.php
```bash
Exmaple:
 'from' => ['address' => 'laravel@laravel.com', 'name' => 'LaravelDev'],
```
See www.laravel.com/docs/master/mail for more info about mail settings.

##### Using own email template for password reset mail.
Change the view route inside -> config/entrance.php
```bash
'mail' => [
 			'password_reset' => '<your view here>'
 		]
```

#### Authenticate Routes
Add all the routes into this group that requires the users to be logged in.
```bash
Route::group(['middleware' => 'checklogin'], function() {
    <Your routes>
});
```

##### Insert basic users (dont forget to change password)
put the following seeds to database/seeds/DatabaseSeeder.php in the run() function<br>
```bash
$this->call(MainUserSeed::class);
```
Run
```bash
artisan db:seed
```

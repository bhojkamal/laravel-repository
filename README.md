# A basic light weight package to implement Repository Design Pattern in Laravel.

[![Latest Version on Packagist](https://img.shields.io/packagist/v/jobins/laravel-repository.svg?style=flat-square)](https://packagist.org/packages/jobins/laravel-repository)
[![GitHub Tests Action Status](https://img.shields.io/github/workflow/status/jobins/laravel-repository/run-tests?label=tests)](https://github.com/jobins/laravel-repository/actions?query=workflow%3Arun-tests+branch%3Amain)
[![GitHub Code Style Action Status](https://img.shields.io/github/workflow/status/jobins/laravel-repository/Check%20&%20fix%20styling?label=code%20style)](https://github.com/jobins/laravel-repository/actions?query=workflow%3A"Check+%26+fix+styling"+branch%3Amain)
[![Total Downloads](https://img.shields.io/packagist/dt/jobins/laravel-repository.svg?style=flat-square)](https://packagist.org/packages/jobins/laravel-repository)

This is where your description should go. Limit it to a paragraph or two. Consider adding a small example.

## Support us

[<img src="https://github-ads.s3.eu-central-1.amazonaws.com/laravel-repository.jpg?t=1" width="419px" />](https://spatie.be/github-ad-click/laravel-repository)

We invest a lot of resources into creating [best in class open source packages](https://spatie.be/open-source). You can support us by [buying one of our paid products](https://spatie.be/open-source/support-us).

We highly appreciate you sending us a postcard from your hometown, mentioning which of our package(s) you are using. You'll find our address on [our contact page](https://spatie.be/about-us). We publish all received postcards on [our virtual postcard wall](https://spatie.be/open-source/postcards).

## Installation

You can install the package via composer:

```bash
composer require puncoz/laravel-repository
```

You can publish and run the migrations with:

```bash
php artisan vendor:publish --tag="laravel-repository-migrations"
php artisan migrate
```

You can publish the config file with:

```bash
php artisan vendor:publish --tag="laravel-repository-config"
```

This is the contents of the published config file:

```php
return [
];
```

Optionally, you can publish the views using

```bash
php artisan vendor:publish --tag="laravel-repository-views"
```

## 🔌 Repository Binding (Service Provider Setup)
To auto-bind your repositories and interfaces, register the RepositoryServiceProvider.

### 🧩 Step 1: Add Binding Config
Create a file at config/bindings/repositories.php:

```php
<?php

use App\Repositories\Auth\Interfaces\UserRepositoryInterface;
use App\Repositories\Auth\UserRepository;

return [
    UserRepositoryInterface::class => UserRepository::class,
];
```
You can add as many repository bindings here as needed.

## 🛠 Step 2: Register Bindings in the Service Provider
Update your RepositoryServiceProvider like so:

```php
<?php

namespace App\Providers;

use Illuminate\Support\ServiceProvider;

class RepositoryServiceProvider extends ServiceProvider
{
    public function register(): void
    {
        /**
         * @var array<string, string> $bindings
         */
        $bindings = config('bindings.repositories');

        collect($bindings)->each(function (string $implementation, string $contract) {
            $this->app->bind($contract, $implementation);
        });
    }
}
```
## ⚙️ Step 3: Register Service Provider (Laravel 11/12)
In Laravel 11 and 12, manually register your service provider in bootstrap/providers.php:
```php
return [
    // Other service providers...
    App\Providers\RepositoryServiceProvider::class,
];
```

### ✅ Ready to rock!
Now, Laravel will automatically resolve the correct repository implementation via the interface wherever it's type-hinted using constructor injection or service container resolution.

## ⚙️ New Artisan Commands
This package now includes three powerful Artisan commands to help scaffold Repositories, 
Transformers, and Filters with minimal effort.

### 🔧 Configuration 
You can customize the default paths via the config file located at: config/config.php

```php
return [
    'repository_path' => env('REPOSITORY_PATH', base_path('app/Repositories')),
    'interface_subfolder' => env('REPOSITORY_INTERFACE_SUBFOLDER', false),

    'transformer_path' => env('TRANSFORMER_PATH', 'app/Http/Transformers'),
    'filter_path' => env('FILTER_PATH', 'app/Http/Filters'),
];
```
## 📦 make:repository

* interface_subfolder:

* If true, the interface will be placed in an Interfaces/ subfolder.

* If false, it will be placed in the same folder as the repository.

## Generate Repository and Interface as same time with:

```bash
php artisan make:repository {name}
```

### Example

```bash
php artisan make:repository product/stock 
```

This will generate:

* app/Repositories/Product/StockRepository.php

* app/Repositories/Product/Interfaces/StockRepositoryInterface.php (if interface_subfolder is true)

* Or app/Repositories/Product/StockRepositoryInterface.php (if false)

It automatically handles:

* Folder creation

* Proper naming conventions

* Namespace and use statements

## 🔄 make:transformer

Generate a Transformer class.
```bash
php artisan make:transformer {name}
```

### Example
```bash
php artisan make:transformer product/stock
```
### ✅ This will generate:

* app/Http/Transformers/Product/StockTransformer.php

## 🔍 make:filter
Generate a Filter class for Eloquent query filtering.

```bash
php artisan make:filter {name}
```

### Example
```bash
php artisan make:filter product/stock
```

### ✅ This will generate:

* app/Http/Filters/Product/StockFilter.php


### 🧠 💡 Notes

* Slashes (/) in names are used to create subdirectories automatically.

* All files are created with proper namespaces and boilerplate code to get you started instantly.

* You can override default paths using the config file or environment variables.

## Usage

```php
$laravelRepository = new JoBins\LaravelRepository();
echo $laravelRepository->echoPhrase('Hello, JoBins!');
```

## Testing

```bash
composer test
```

## To produce file
register this in RepositoryServiceProvider.php
```bash
// Register console commands only if running in the console in register.
if ($this->app->runningInConsole()) {
    $this->commands([
        \JoBins\LaravelRepository\Console\Commands\MakeRepositoryCommand::class,
    ]);
}
```    

## Changelog

Please see [CHANGELOG](CHANGELOG.md) for more information on what has changed recently.

## Contributing

Please see [CONTRIBUTING](.github/CONTRIBUTING.md) for details.

## Security Vulnerabilities

Please review [our security policy](../../security/policy) on how to report security vulnerabilities.

## Credits

- [Puncoz Nepal](https://github.com/puncoz)
- [All Contributors](../../contributors)

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.

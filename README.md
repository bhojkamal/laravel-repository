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
composer require jobins/laravel-repository
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

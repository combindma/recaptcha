# Google reCAPTCHA V3 Package

[![Latest Version on Packagist](https://img.shields.io/packagist/v/combindma/recaptcha.svg?style=flat-square)](https://packagist.org/packages/combindma/recaptcha)
[![GitHub Tests Action Status](https://img.shields.io/github/actions/workflow/status/combindma/recaptcha/run-tests.yml?branch=main&label=tests&style=flat-square)](https://github.com/combindma/recaptcha/actions?query=workflow%3Arun-tests+branch%3Amain)
[![GitHub Code Style Action Status](https://img.shields.io/github/actions/workflow/status/combindma/recaptcha/fix-php-code-style-issues.yml?branch=main&label=code%20style&style=flat-square)](https://github.com/combindma/recaptcha/actions?query=workflow%3A"Fix+PHP+code+style+issues"+branch%3Amain)
[![Total Downloads](https://img.shields.io/packagist/dt/combindma/recaptcha.svg?style=flat-square)](https://packagist.org/packages/combindma/recaptcha)


Simple and painless Google reCAPTCHA V3 package for Laravel framework.

Inspired by: https://github.com/biscolab/laravel-recaptcha

## Installation

You can install the package via composer:

```bash
composer require combindma/recaptcha
```

You can publish the config file with:
```bash
php artisan vendor:publish --provider="Combindma\Recaptcha\RecaptchaServiceProvider" --tag="recaptcha-config"
```

This is the contents of the published config file:

```php
return [

    //The name of the input used to send Google reCAPTCHA token to verify
    'token_name' => env('RECAPTCHA_NAME', 'recaptcha_token'),

    /**
     *
     * The site key
     * get site key @ www.google.com/recaptcha/admin
     *
     */
    'api_site_key' => env('RECAPTCHA_SITE_KEY', ''),

    /**
     *
     * The secret key
     * get secret key @ www.google.com/recaptcha/admin
     *
     */
    'api_secret_key' => env('RECAPTCHA_SECRET_KEY', ''),

    /**
     *
     * The curl timout in seconds to validate a recaptcha token
     *
     */
    'curl_timeout' => 10,

    /**
     *
     * Set API domain. You can use "www.recaptcha.net" in case "www.google.com" is not accessible.
     * (no check will be made on the entered value)
     * @see   https://developers.google.com/recaptcha/docs/faq#can-i-use-recaptcha-globally
     * @since v4.3.0
     * Default 'www.google.com' (ReCaptchaBuilder::DEFAULT_RECAPTCHA_API_DOMAIN)
     *
     */
    'api_domain' => 'www.google.com',

    //you can disable the ReCaptcha when you test your application
    'enabled' => env('RECAPTCHA_ENABLED', 'true'),
    
];
```

You can publish the translations file with:
```bash
php artisan vendor:publish --provider="Combindma\Recaptcha\RecaptchaServiceProvider" --tag="recaptcha-translations"
```

This is the contents of the published translations file:

```php
return [
    'invalid' => 'We could not verify if you are a robot or not. Please refresh the page.',
];
```
## Usage

### Embed in Blade
Insert htmlScriptTagJsApi($config) helper before closing </head> tag.
```html
<!DOCTYPE html>
<html>
<head>
    {!! htmlScriptTagJsApi(['action' => 'homepage']) !!}
</head>
```

Insert recaptchaInput() helper inside your form tag.
```html
<form action="" method="POST">
    @csrf
    {!! recaptchaInput() !!}
    <!-- More inputs -->
</form>
```

### Validate the token 

Add the rule 'recaptcha' in your validation rules request or in your controller 
```php
 
 $request->validate([
       //... other rules
       
       //Add this to your validation rule
       config('recaptcha.token_name') => ['required','string', 'recaptcha']
       ]);
```
If the validation fails, an error will be returned.

## Testing

```bash
composer test
```

## Contributing

Please see [CONTRIBUTING](.github/CONTRIBUTING.md) for details.

## Security Vulnerabilities

Please review [our security policy](../../security/policy) on how to report security vulnerabilities.

## Credits

- [Combind](https://github.com/Combind)
- [All Contributors](../../contributors)

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.

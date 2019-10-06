# Laravel Package for Vodacom Mozambique M-Pesa

**PLEASE, READ THIS. THANK YOU**

This package is a wrapper for abdulmueid/mpesa-php-api to integrate M-Pesa API in Laravel applications

For more information of what's M-Pesa, please refer to M-Pesa official website:
**https://www.vm.co.mz/en/M-Pesa2**

# This package is still in development, so don't use it in production

# 1. Installation

All that you have to do is the following:

# The code isn't in packagist (https://packagist.org) yet.

```
composer require calvinchiulele/mpesa-mz
```

```
php artisan vendor:publish --providor=calvinchiulele\MPesaMz\Providers\MPesaMzServiceProvider --tag=config
```

# 2. Usage

After you have published the config files necessary for the packages, you've to customize it according to your needs:

```
return [
    /*
    |--------------------------------------------------------------------------
    | Public key for use in M-Pesa API
    |--------------------------------------------------------------------------
    |
    | Here you may specify the public key provided by Vodacom to you
    |
    */
    'public_key' => env('MPESA_PUBLIC_KEY', null),

    /*
    |--------------------------------------------------------------------------
    | API host of M-Pesa API
    |--------------------------------------------------------------------------
    |
    | Here you may specify the API host provided by Vodacom for API operations
    |
    */
    'api_host' => env('MPESA_API_HOST', 'api.sandbox.vm.co.mz'),

    /*
    |--------------------------------------------------------------------------
    | API Key of M-Pesa API
    |--------------------------------------------------------------------------
    |
    | Here you may specify the API key provided by Vodacom to you
    |
    */
    'api_key' => env('MPESA_API_KEY', null),

    /*
    |--------------------------------------------------------------------------
    | Origin of M-Pesa API
    |--------------------------------------------------------------------------
    |
    | Here you may specify the API key provided by Vodacom to you
    |
    */
    'origin' => env('MPESA_ORIGIN', null),

    /*
    |--------------------------------------------------------------------------------------
    | Service Provider Code of M-Pesa API
    |--------------------------------------------------------------------------------------
    |
    | Here you may specify the service provider code of M-Pesa provided by Vodacom to you
    |
    */
    'service_provider_code' => env('MPESA_SERVICE_PROVIDER_CODE', null),

    /*
    |--------------------------------------------------------------------------
    | Initiator Identifier of M-Pesa API
    |--------------------------------------------------------------------------
    |
    | Here you may the initiator identifier provided by Vodacom to you
    |
    */
    'initiator_identifier' => env('MPESA_INITIATOR_IDENTIFIER', null),

    /*
    |--------------------------------------------------------------------------
    | Security credential of M-Pesa API
    |--------------------------------------------------------------------------
    |
    | Here you may specify the security credential provided by Vodacom to you
    |
    */
    'security_credential' => env('MPESA_SECURITY_CREDENTIAL', null)
];
```

The part that I'm proud of, is located at:
```
src/Services/MpesaMz.php - line 35 to 45

35    /**
36     * Forwards the calls to transaction
37     *
38     * @param $name
39     * @param $arguments
40     * @return mixed
41     */
42    public function __call($name, $arguments)
43    {
44        return call_user_func_array([$this->transaction, $name], $arguments);
45    }

I implemented the Proxy design pattern to delegate all the requests of that 
class to \abdulmueid\mpesa\Transaction, a class which is responsabile to manage all
requests related M-Pesa API. I also used the Single Responsability Principle in the design
of that class

```


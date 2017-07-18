# API Manager

API manager is a PHP API Client Development Kit. You can easily handle all kind of JSON api response by using this package.

## Requirements

- PHP >= 5.5.9

## Installations

```shell
composer require nahid/api-manager
```

## Configurations

There are no extra configuration for this package.

## Usage

Lets make a api service service for https://reqres.in.

Suppose you have to make several api service for your package. Your service directory is
`app/Services`. Now we are develop a service for https://reqres.in and make a class file `ReqResApiService.php`
which is extend by `\ApiManager\AbstractApi` class.

```php
namespace App\Services;

use ApiManager\AbstractApi;

class ReqResApiService extends AbstractApi
{
    protected function setBaseUrl(): string
    {
        return 'https://reqres.in';
    }
}
```

`AbstractApi` is a abstract class where `setBaseUrl()` is a abstract method.

To get API response from this url they've a prefix 'api' so first we set it with protected property `$prefix`

```php
namespace App\Services;

use ApiManager\AbstractApi;

class ReqResApiService extends AbstractApi
{
    protected $prefix = 'api';

    protected function setBaseUrl(): string
    {
        return 'https://reqres.in';
    }
}
```

Now we make a method for get all users info

```php
namespace App\Services;

use ApiManager\AbstractApi;

class ReqResApiService extends AbstractApi
{
    protected $prefix = 'api';

    protected function setBaseUrl(): string
    {
        return 'https://reqres.in';
    }

    public function allUsers()
    {
        $users = $this->get('/users');

        if ($users->getStatusCode() == 200) {
            return $users;
        }

        return false;
    }
}
```

We use GuzzleHttp for this package. So you can easily use all HTTP verbs
 from as a method from PHP magic method. Its totally hassle free. with our all response we return three object `response`, `request` and `contents`.
 You can access all Guzzle response method from this response. We are using magic method to access it.

#### Output

![Response](http://imgur.com/IgI0vKb.png?1 "Response")


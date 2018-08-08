---
layout: project
version: 3.x
title: HTTP Responses
---
# HTTP Responses

* [Instantiation](#instantiation)
* [Immutability](#immutability)
* [Working with response headers](#working-with-response-headers)
* [Handling cookies](#handling-cookies)
* [Response body](#response-body)
* [Other methods](#other-methods)

## Instantiation

An HTTP response is represented with the help of the `Opis\Http\Response` class, 
or by using a class that inherits from the `Opis\Http\Response` class. 
The constructor of the class has the following signature.

```php
public function __construct(
    int $statusCode = 200, 
    array $headers = [], 
    IStream $body = null, 
    string $protocolVersion = 'HTTP/1.1'
);
```

* `$statusCode` - response status code
* `$headers` - a key-value mapped array of headers, where the key represents the header's name and the value
represents the actual value of the header
* `$body` - the response body, if any
* `$protocolVersion` - the protocol version number

## Immutability

By default, all response instances are designed to be immutable. 
This design choice was made in order to prevent an HTTP response for being unintentionally modified.
If you want to modify the response (e.g. add a cookie), then you must use the `modify` method.
This method returns a cloned version of the original response object, that reflects the changes you've made.

```php
use Opis\Http\Response;

// ..

$response = $response->modify(function(Response $response){
    // add headers, set status code, add new cookies, etc.
});
```

## Working with response headers

Adding a new header is done with the help of the `setHeader` method.
Because of the immutable nature of the response object, trying to call this method
directly, will result into an exception being thrown. Instead, you must use the `modify` method.

```php
// will throw exception
$response->setHeader('X-Foo', 'Bar');

// The right way to do it
$response = $response->modify(function(Response $response){
    $response->setHeader('X-Foo', 'Bar');
    $response->setHeader('X-Bar', 'Baz');
});
```

Setting multiple headers at the same time can be accomplished by using the `addHeaders` method.

```php
$response = $response->modify(function(Response $response){
    $response->addHeaders([
        'X-Foo' => 'Bar',
        'X-Bar' => 'Baz',
    ]);
});
```

Getting the full list of header is done by calling the `getHeaders` method.

```php
$headers = $response->getHeaders();
```

Reading an individual header is done by passing the header's name to the `getHeader` method.
If the header was not set, `null` will be returned, by default. 

```php
$header = $response->getHeader('Content-Type');
```

If you want to change the default value returned if the specified header was not found, then you must
simply pass a second argument to the `getHeader` method.

```php
$header = $response->getHeader('Content-Type', 'text/html');
```

Checking if a header was set, is done by using the `hasHeader` method.

```php
if ($response->hasHeader('Content-Type')) {
    // do something
}
```

## Handling cookies

Setting a new cookie is done with the help of the `setCookie` method.

```php
$resposne = $response->modify(function(Response $response){
    // set a cookie named 'foo', having a value 'bar'
    $response->setCookie('foo', 'bar');
});
```

The better explain the `setCookie` method, let's analise its signature.

```php
public function setCookie(
    string $name,
    string $value = '',
    int $expire = 0,
    string $path = '',
    string $domain = '',
    bool $secure = false,
    bool $http_only = false
): self;
```

* `$name` - the name of the cookie
* `$value` - the value of the cookie
* `$expire` - a UNIX timestamp that tells when this cookie is set to expire. 
* `$path`  - tells on which path this cookie is valid
* `$domain` - 
* `$secure` -
* `$http_only` - 


Getting the full list of cookies is done by calling the `getCookies` method.

```php
$cookeis = $response->getCookies();
```

If you want to check if a cookie was set or not, simply use the `hasCookie` method.
You can optionally specify a domain and a path, and check if a cookie was set for the
specified domain and path. 

```php
if ($response->hasCookie('foo')) {
    // do something
}

if ($response->hasCookie('foo', '/some/path/')) {
    // do something
}

if ($response->hasCookie('foo', '', 'www.domain.com')) {
    // do something
}

if ($response->hasCookie('foo', '/some/path/', 'www.domain.com')) {
    // do something
}
```

Removing a cookie is done by using the `clearCookie` method.

```php
$response = $response->modify(function(Response $response){
    $response->clearCookie('foo');
    $response->clearCookie('foo', '/some/path/');
    $response->clearCookie('foo', '', 'www.domain.com');
    $response->clearCookie('foo', '/some/path/', 'www.domain.com');
});
```

You can remove all cookies by using the `clearCookies` method;

```php
$response = $response->modify(function(Response $response){
    $response->clearCookies();
});
```

## Response body

You can access the response body by calling the `getBody` method. This method returns an instance of `Opis\Http\Stream`,
or `null` if the response message has no body.

```php
if (null !== $body = $response->getBody()) {
    // do something
}
```

You can set the response body by calling the `setBody` method.

```php
$response = $response->modify(function(Response $response){
    $response->setBody(null);
    // or
    $response->setBody(new Stream("php://temp", "wb+"));
});
```

## Other methods

Reading the protocol version number is done by using the `getProtocolVersion` method.
You can modify the protocol version number by calling the `setProtocolVersion` method.

```php
$version = $response->getProtocolVersion();

$response = $response->modify(function(Response $response){
    $response->setProtocolVersion('HTTP/1.1');
});
```

Modifying the response status code is done by using the `setStatusCode` method.
You can read the current status code with the help of the `getStatusCode` method.

```php
$code = $response->getStatusCode();

$response = $response->modify(function(Response $response){
    $response->setStatusCode(200);
});
```



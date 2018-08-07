---
layout: project
version: 3.x
title: HTTP Responses
---
# HTTP Responses

* [Instantiation](#instantiation)

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

By default, all response instances are designed to be immutable. This design choice was made in order to prevent
a response for being modified

```php
use Opis\Http\Response;

// ..

$response = $response->modify(function(Response $response){
    // add headers, set status code, or add new cookies
});
```
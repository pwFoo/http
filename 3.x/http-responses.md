---
layout: project
version: 3.x
title: HTTP Responses
---
# HTTP Responses

A response is represented by using an instance of the `Opis\Http\Response` class, or an instance of a class that
extends it. The constructor of the class has the following signature.

```php
public function __construct(
    int $statusCode = 200, 
    array $headers = [], 
    IStream $body = null, 
    string $protocolVersion = 'HTTP/1.1'
);
```
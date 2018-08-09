---
layout: project
version: 3.x
title: Response types
---
# Response types

* [String response](#string-response)
* [Html response](#html-response)
* [Json response](#json-response)
* [File stream](#file-stream)
* [File download](#file-download)
* [Redirect response](#redirect-response)
* [Empty response](#empty-response)

## String response

This type of response is represented with the help of the `Opis\Http\Responses\StringResponse` class and it allows you to
send a string as an HTTP response. 
The signature of the class' constructor looks like below:

```php
public function __construct(string $body, int $status = 200, array $headers = [])
```

* `$body` - the message body
* `$status` - response status code
* `$headers` - a list of headers

By default, this class automatically ads a `Content-Length` header to the response.

```php
use Opis\Http\Responses\StringResponse;

$response = new StringResponse('Hello');

echo $response->getHeader('Content-Length'); //> 5
```

## Html response
## Json response
## File stream
## File download
## Redirect response
## Empty response
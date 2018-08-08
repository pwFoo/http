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

This type of response is represented with the help of the `Opis\Http\Response\StringResponse` and allows you to
send a string as an HTTP response. By default, this class automatically ads a `Content-Length` header to the response.
Here is the signature of the class' constructor.

```php
public function __construct(string $body, int $status = 200, array $headers = [])
```

## Html response
## Json response
## File stream
## File download
## Redirect response
## Empty response
---
layout: project
version: 3.x
title: About
description: Getting started with Opis Http
lib: 
    name: opis/http
    version: 3.0
---
# Http abstraction layer

**Opis Http** is a library that provides an implementation for [PSR-7 Http Message].

## License

**Opis Http** is licensed under [Apache License, Version 2.0][apache_license].

## Requirements

* PHP ^7.0
* [PSR-7 Http Message] ^1.0

## Installation

**Opis Http** is available on [Packagist] and it can be installed from a 
command line interface by using [Composer]. 

```bash
composer require {{page.lib.name}}
```

Or you could directly reference it into your `composer.json` file as a dependency

```json
{
    "require": {
        "{{page.lib.name}}": "^{{page.lib.version}}"
    }
}
```


[apache_license]: http://www.apache.org/licenses/LICENSE-2.0 "Project license" 
{:rel="nofollow" target="_blank"}
[Packagist]: https://packagist.org/packages/{{page.lib.name}} "Packagist" 
{:rel="nofollow" target="_blank"}
[Composer]: http://getcomposer.org "Composer" 
{:ref="nofollow" target="_blank"}
[PSR-7 Http Message]: https://github.com/php-fig/http-message "PSR-7"
{:ref="nofollow" target="_blank"}
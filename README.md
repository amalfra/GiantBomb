PHP wrapper for Giantbomb API
==============================
[![GitHub release](https://img.shields.io/github/release/amalfra/GiantBomb.svg)](https://github.com/amalfra/GiantBomb/releases)

A library for easy interaction with Giantbomb API. Features are:
* PSR-4 autoloading support
* Caching support

> Get your API Key at http://api.giantbomb.com

## Requirements
* PHP >= 7.0
* PHP Redis extension

## Installation
via Composer
```sh
$ composer require giantbomb/giantbomb
```
This will create a vendor directory (if you dont already have one) and set up the autoloading classmap.

## Usage
Once everything is installed, you should be able to load the composer autoloader in your code.

You can load the wrapper classes using namespace as:

```php
require __DIR__ . '/vendor/autoload.php';

use GiantBomb\GiantBomb;
```

Now create a new object

```php
$gb_obj = new GiantBomb('YOUR_KEY');
```

Now the available API methods can be called using the instance. All the result from API will be returned as an object. If any status code other than 200 is returned an exception would be thrown.

### Currently Available Methods
* game(game_id, field_list)
* games(filter, limit, offset, platform, sort, field_list)
* review(review_id, field_list)
* game_rating(rating_id, field_list)
* company(company_id, field_list)
* character(character_id, field_list)
* search(query, field_list, limit, page, resources)
* genres(field_list, limit, offset)
* platforms(field_list, limit, offset, filter, sort)

### Cache
You can configure caching to prevent hitting API if same queries are made again. Currently supported caching methods are:
* inmemory: cache will be stored in memory array. This won't be persisted after your script exits.
* redis: cache will be stored in redis store which can be configured.

Cache can be configured using ```setCacheProvider``` method of GiantBomb instance. If it's not configured caching will be disabled and API will always be hit each time a method is called. ```setCacheProvider``` method accepts two parameter: 
1. [required] cache type eg: inmemory, redis etc
2. [optional] an associative array in which additional configuration details required for setting up the cache method can be given eg: redis server host and port values

#### using inmemory cache method
This method does not need any additional configuration option than just activating by calling ```setCacheProvider``` method with ```inmemory``` as first parameter.
eg:
```php
$gb_obj->setCacheProvider('inmemory');
```
#### using redis cache method
This method can be activated by calling ```setCacheProvider``` method with ```redis``` as first parameter. You will also need to specify redis server host and port as second parameter.
eg:
```php
$gb_obj->setCacheProvider('redis', array('host' => 'localhost', 'port' => 6379));
```

## Development

Questions, problems or suggestions? Please post them on the [issue tracker](https://github.com/amalfra/GiantBomb/issues).

You can contribute changes by forking the project and submitting a pull request. Feel free to contribute :heart_eyes:

UNDER MIT LICENSE
=================

The MIT License (MIT)

Copyright (c) 2013 Amal Francis

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.


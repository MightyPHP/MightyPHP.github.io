---
layout: docs
title: Route
---
# Routing

Routing in MightyPHP uses the routing blocks. Routing blocks are chunks of declarations of request method, path and its endpoint.

### Basic Routing

MightyPHP routing supports RESTful routing, with the basic 4 types of routes:
- ROUTE::get()
- ROUTE::post()
- ROUTE::put()
- ROUTE::delete()

#### Example
In your `Configs/routes.php`, define your routes accordingly:

```php
ROUTE::get('/','controller@homeView');
ROUTE::post('/login','login@authenticate');
```

The second parameter houses the destination, with the syntax of `controller@method`. The controller is without the suffix of "Controller". However, in actual fact, the controller classes in should be suffixed with "Controller".

### Route Naming
You can provide names to routes, which will make it easier to keep track. With a name, routes can be declared in view files using `{% raw %}{{ route(route_name_here) }}{% endraw %}`.

```php
ROUTE::get('/','controller@homeView')->name('home_view');
```

### Route Grouping
For the sake of organization, you may group your routes with the grouping block.

```php
ROUTE::group('/foo', function(){
    ROUTE::get("/", "foo@bar");
    ROUTE::get("/foo", "foo@bar");
    ROUTE::get("/bar", "foo@bar");
});
```

Groupings can be made layers down. A group can exist within a group, for a drill down effect.

### Security Block

If you want your routes to be secure, you can put them under the secureblock.

```php
ROUTE::secure(function(){
    ROUTE::get("/secure", "foo@bar");
    ROUTE::get("/secure2", "foo@bar");
});
```

Routes within these blocks will pass through MightyPHP's security for authentication purposes.

### Middleware Block

If you wish your routes to be filtered by a middleware, you can register them within a middleware block.

```php
ROUTE::middleware(['kickAss'], function(){
	ROUTE::get("/", "foo@bar");
});
```

You may have more than one middleware injection, by appending to the array. The middlewares are administered by order. So whichever middleware you want to administer first, put it as first, and vice versa. You can have more than 2.

```php
ROUTE::middleware(['kickAss', 'kickass2', 'block'], function(){
	ROUTE::get("/", "foo@bar");
});
```
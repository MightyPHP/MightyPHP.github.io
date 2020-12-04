---
layout: blog
title:  "Release of v1.0.0"
date:   2020-12-04 16:23:32 +0800
categories: blog
---
<h1>The first official production version of MightyPHP!</h1>

After months of working 0.x.x versions, the decision to fix on some standard features and functions was made in early and mid 2020. With some tweaking, the first production ready version is ready.

## What's new?
This list is not exhaustive and only serves as a highlight of changes that I deem to be major.

### Scoped routes
``` php
use MightyCore\Routing\Router;

// This is a scope
$router = new Router('/');

$router->get('/', 'HomeController@view');
```
I have decided to ditch the routing blocks from 0.x.x versions, and created a scoped based routing. This is syntatically cleaner, easier to read, and makes us all happier.

### Elegant Controllers
Request and response objects and how they interact with controllers have been revamped. 

Requests are now injected as a dependency to each controller, making it more elegant. Each parameters embeded by URL slashes are now controller method parameters, as opposed to `params` array in previous version.

``` php
namespace Application\Controllers;

use Application\Controllers\Controller;
use MightyCore\Http\Request;

class FooController extends Controller
{
    public function getAge(Request $request){
        return $request->query("age");
    }

    // www.example.com/bob/dylan?age=12
    public function bar(Request $request, $name, $lastName){
        echo $request->query("age"); // 12
        echo $name; // bob
        echo $lastName; // dylan
    }
}
```

Response objects are syntatically sweeter. Setting headers, and response code can be made to the response object, instead of using static classes as previously done.

``` php
 public function bar(Response $response, $name){
    $response->header("FOOBAR", $name)
    $response->send("I am ".$name);
}
```

### The merging of Model and Storage
In 0.x.x versions, Models and Storages co-exist and worked well together. After much consideration, it is decided that the Storage's query builder feature will be merged into Model, and serve as the de-facto way of writing Models. 

### Schematics for migrations
I am looking forward to integrating more databases, mainly Postgres in the near future. With that, I had prepared the migration schematic to allow cross-database migrations. As of now the syntax is similar to that used by Laravel's but it may change to fit our solution as it is developed further.

``` php
use \MightyCore\Database\Schema;
use \MightyCore\Database\Schematic;
             
class _2020_05_28_150843_create_users_table{
    public $timestamp=1590678523;
    public $connection="default";
    public function up(){
        return [
            Schema::create('users', function(Schematic $table){
                $table->integer('users_id')->increments();
                $table->varchar('users_password', 255);
                $table->varchar('users_email', 255);
                $table->datetime('users_createdAt');
                $table->datetime('users_modifiedAt');
                $table->tinyint('users_deleted', 1)->default(0);
            })
        ];
    }

    public function down(){
        return [
            Schema::drop('users')
        ];
    }
}
```

### The long overdue console commands
I had extended the `php mighty` commands to include more, such as code scaffolding. You may now run `php mighty make:controller UserController`, which will generate a ready to use controller under the Application/Controllers folder.

You may explore other useful console commands in the documentations, of which we may add on from time to time.

### Many more to come
Since the 0.x.x versions of the framework, I had been testing it in small scale private projects. There are certainly many plans in the pipeline which I hope to deliver in the shortest time possible.
---
layout: docs
title: Storage
---
The STORAGE module is to make working with databases that much easier, by writing as little raw queries as you can. Of course, you can still work with Mighty Models and write raw queries to have a better control. 

To use a store, you must first initialize the table with the `store()` method: 
``` php
/* this initializes the user table */
STORAGE::store('user')
```

### `create()`

The `create()` method is a perfect method for writing insert queries. The method takes in 2 parameters: 
- Query parameters (array)
- Exit on exist (boolean)
  
```php
STORAGE::store('user')->create(array(
    "name" => 'Bob',
    "age" => 14,
    "username" => 'Bob14'
));
```

The `create()` method will first check for existing records based on the query parameters. If a record exists, it will automatically update the new record, else it will insert a new record.

You may also have it fail if a record already existed:

```php
STORAGE::store('user')->create(array(
    "name" => 'Bob',
    "age" => 14,
    "username" => 'Bob14'
), true);
```

By having a true in the second parameter, the method will return false on record exist.
The checking of existing records is fully customisable.  If you wish to not have a column checked for existing records, you may do so like this:

```php
STORAGE::store('user')->create(array(
    "*name" => 'Bob',
    "age" => 14,
    "username" => 'Bob14'
));
```

Notice how there is a `*` prefixed in the name column. This prevents the column with the assigned value to be part of the condition(s) to check for existing records. This could be helpful in preventing unwanted updates, or false results.

### `insert()`
You can also choose to insert records using the `insert()` method.

``` php
STORAGE::store('user')->insert([
    'username' => 'Bob',
    'password' => '123'
]);
```

### `update()`
To update a certain records, use the `update()` method.

``` php
STORAGE::store('user')->update([
    'username' => 'Bob',
    'password' => '123'
]);
```

### `select()`
Select parameters will be injected as raw queries into the query builder. So be careful as to not expose your application to any SQL injections here.

``` php
STORAGE::store('user')->select('name','age','email')->get();
```

To select raw, simply type in as such:
``` php
STORAGE::store('user')->select('COUNT(*) as total')->get();
```

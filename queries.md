# Query Builder

- [Selects](#selects)
- [Joins](#joins)
- [Aggregates](#aggregates)
- [Inserts](#inserts)
- [Updates](#updates)
- [Deletes](#deletes)

## Selects

##### Retrieving All Rows From A Table

```php
$users = DB::table('users')->get();

foreach ($users as $user) {
    var_dump($user->username);
}
```

##### Retrieving A Single Row From A Table

```php
$user = DB::table('users')->where('username', 'john')->first();

var_dump($user->username);
```

##### Retrieving A Single Column From A Row

```php
$username = DB::table('users')->where('username', 'john')->pluck('name');
```

##### Specifying A Select Clause

```php
$users = DB::table('users')->select('username', 'email')->get();

$users = DB::table('users')->distinct()->get();

$users = DB::table('users')->select('name as username')->get();
```

##### Using Where Operators

```php
$users = DB::table('users')->where('id', '>', 10)->get();
```

##### Or Statements

```php
$users = DB::table('users')
                ->where('id', '>', 10)
                ->orWhere('username', 'john')
                ->get();
```

##### Using Where Between

```php
$users = DB::table('users')
                ->whereBetween('id', array(1, 10))->get();
```

##### Using Where In With An Array

```php
$users = DB::table('users')
                ->whereIn('id', array(1, 2, 3))->get();

$users = DB::table('users')
                ->whereNotIn('id', array(1, 2, 3))->get();
```

##### Using Where Null To Find Records With Unset Values

```php
$users = DB::table('users')
                ->whereNull('display_name')->get();
```

#####  Nested Wheres

```php
DB::table('users')
        ->where('username', '=', 'john')
        ->orWhere(function($query) {
            $query->where('id', '>', 10)
                  ->where('status', '=', '1');
        })
        ->get();
```

The query above will produce the following SQL:

```sql
select * from users where username = 'john' or (id > 10 and status = '1')
```

##### Order By
  
```php 
$users = DB::table('users')
                ->orderBy('joined', 'desc')
                ->get();
```

##### Offset & Limit

```php
$users = DB::table('users')->skip(10)->take(5)->get();
```

## Joins

The query builder may also be used to write join statements. Take a look at the following examples:

##### Basic Join Statement

```php
DB::table('users')
        ->join('contacts', 'users.id', '=', 'contacts.user_id')
        ->select('users.id', 'username')
        ->get();
```

##### Left Join Statement

```php
DB::table('users')
    ->leftJoin('roles', 'role_id', '=', 'posts.id')
    ->get();
```

## Aggregates

The query builder also provides a variety of aggregate methods, such as `count`, `max`, `min`, `avg`, and `sum`.

##### Using Aggregate Methods

```php
$users = DB::table('users')->count();

$id = DB::table('users')->max('id');

$id = DB::table('users')->min('id');

$id = DB::table('users')->avg('id');

$id = DB::table('users')->sum('id');
```

## Inserts

##### Inserting Records Into A Table

```php
DB::table('users')->insert(
    array('email' => 'john@example.com', 'status' => 1)
);
```

If the table has an auto-incrementing id, use insertGetId to insert a record and retrieve the id:

##### Inserting Records Into A Table With An Auto-Incrementing ID

```php
$id = DB::table('users')->insertGetId(
    array('email' => 'john@example.com', 'status' => 1)
);
```

##### Inserting Multiple Records Into A Table

```php
DB::table('users')->insert(array(
    array('email' => 'foo@example.com', 'status' => 1),
    array('email' => 'bar@example.com', 'status' => 1),
));
```

## Updates

##### Updating Records In A Table

```php
DB::table('users')
        ->where('id', 1)
        ->update(array('username' => 'foo'));
```

## Deletes

##### Deleting Records In A Table

```php
DB::table('users')->where('id', '<', 10)->delete();
```

##### Deleting All Records From A Table

```php
DB::table('users')->delete();
```

##### Truncating A Table

```php
DB::table('users')->truncate();
```

# Basic Database Usage

- [Configuration](#configuration)
- [Running Queries](#running-queries)

## Configuration

The database configuration file is `app/config/database.php` where you can define the connection details, as well as some other options.

## Running Queries

You can run queries using the `DB` class.

##### Running A Select Query

```php
$users = DB::select('select * from users where id = ?', array(1));
```

The `select` method will always return an array of results.

##### Running An Insert Statement

```php
DB::insert('insert into users (id, email) values (?, ?)', array(1, 'foo@example.com'));
```

##### Running An Update Statement

```php
DB::update('update users set email = "bar@example.com" where id = ? limit 1', array(1));
```

##### Running A Delete Statement

```php
DB::delete('delete from users where id = ?', array(1));
```

##### Running A General Statement

```php
DB::statement('drop table users');
```

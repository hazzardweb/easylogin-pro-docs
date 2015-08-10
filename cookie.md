# Cookie

#### Storing An Item In The Cookie

```php
Cookie::set('key', 'value');
```

#### Retrieving An Item From The Cookie

```php
$value = Cookie::get('key');
```

#### Determining If An Item Exists In The Cookie

```php
if (Cookie::has('key')) {
    //
}
```

See `src/Hazzard/Cookie/CookieJar.php` for the full list of methods.

# Cookie

#### Storing An Item In The Cookie

    Cookie::set('key', 'value');

#### Retrieving An Item From The Cookie

    $value = Cookie::get('key');

#### Determining If An Item Exists In The Cookie

    if (Cookie::has('key')) {
        //
    }

See `src/Hazzard/Cookie/CookieJar.php` for the full list of methods.
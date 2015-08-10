# User

- [User Model](#user-model)
- [User Meta](#user-meta)

## User Model

The `User` class (stored in `app/models`) is a "Model" allowing to interact with the `users` table. 

>Notice: This page is dedicated to `User` class specifics and NOT how to add, get, update or delete users. <br> For that read about [Models](models.md).

Given a `$user` of type `User` access the attributes like this:

```php
$user_id = $user->id;
$username = $user->username;
```

The default attributes are: `id`, `username`, `email`, `password`, `display_name`, `joined`, `status`, `role_id`. 

However there are some extra ones: `avatar`, `firstName`, `lastName`, `about`, `gender`, `birthday`, `phone`, `location`, `verified`, `lastLogin`, `lastLoginIp`.

If you have set some other ones using the [User Fields](userfields.md) or [User Meta](usermeta.md) you can access them using the `usermeta` attribute:

```php
$value = $user->usermeta['meta_key'];
```

Make sure to wrap that in a `if` statement or use `@` for safety.

You may use the `User::can` method to determine if a user has a specific permission.

```php
if ($user->can('add_users')) {
    // The user can add users
}
```

## User Meta

The User Meta allows to simply add, get, update and delete custom meta for the users.

#### Adding Metadata To A User

```php
Usermeta::add('user_id', 'meta_key', 'meta_value', true);
```

The last argument indicates whether the same key should not be added.

#### Retrieving Metadata For A User.

```php
$value = Usermeta::get('user_id', 'meta_key', true);
```

If the second argument is empty `''` all metadata for the user will be retrieved.
The last argument indicates whether to return a single value for the key.

#### Updating Metadata For A User.

```php
Usermeta::update('user_id', 'meta_key', 'meta_value');
```

#### Removing Metadata For A User.

```php
Usermeta::delete('user_id', 'meta_key');
```
If the second argument is omitted all metadata for the user will be removed.

See `src/Hazzard/User/Meta.php` for the full list of methods and arguments for the `Usermeta` class.

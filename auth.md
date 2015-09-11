# Authentication

- [Configuration](#configuration)
- [Authenticating Users](#authenticating-users)
- [Registering & Activation](#registering-&-activation)
- [Password Reminders & Reset](#password-reminders-&-reset)
- [Social Authentication](social-auth.md)

## Configuration

The authentication configuration file is located at `app/config/auth.php` which contains all of the well documented options for authentication.

## Authenticating Users

To log a user into your website, you may use the `Auth::login` method.

```php
if (Auth::login($emailOrUsername, $password, true)) {
    redirect_to('index.php');
}
```

The third argument must be boolean, `true` or `false` and indicates if the user should be rememember using the browser cookie. By default is `false`.

If the authentication is successful, the `auth.login` event will be fired in `app/events.php`.

For a complete example see `code/versions/basic/login.php` from the archive.

#### Determining If A User Is Authenticated

To determine if the user is already logged into your website, you may use the `Auth::check` method:

```php
if (Auth::check()) {
    // You are logged in...
}

if (Auth::guest()) {
    // You are not logged in...
}
```

#### Accessing The Logged In User

Once a user is authenticated, you may access the user attributes:

```php
$email = Auth::user()->email;
```

The default attributes are: `id`, `username`, `email`, `password`, `display_name`, `joined`, `status`, `role_id`. 

However there are some extra ones: `avatar`, `firstName`, `lastName`, `about`, `gender`, `birthday`, `phone`, `location`, `verified`, `lastLogin`, `lastLoginIp`.

If you have set some other ones using the [User Fields](userfields.md) or [User Meta](usermeta.md) you can access them using the `usermeta` attribute:

```php
$value = Auth::user()->usermeta['meta_key'];
```

Make sure to wrap that in a `if` statement or use `@` for safety.

#### Determining If A User Has A Permission

To determine if the user has a specific permission, you may use the `Auth::userCan` method.

```php
if (Auth::userCan('add_users')) // <=> Auth::user()->can('add_users') {
    // You can add users
}
```

The available permissions are: `dashboard`, `add_users`, `list_users`, `edit_users`, `delete_users`, `message_users`, `manage_roles`, `manage_fields`, `manage_settings`, `moderate`.

#### Logging A User Out Of The Application

```php
Auth::logout();
```

After logout the `auth.logout` event will be fired in `app/events.php`.

#### Logging In Users By ID

```php
$user = User::find(1);

Auth::loginById($user->id);
```

See `src/Hazzard/Auth/Auth.php` for the full list of methods and arguments.

## Registering & Activation

#### Registering Users

To register a user into your website, you may use the `Register::signup` method.

```php    
$data = array(
    'email' => 'foo@example.com', 
    'username' => 'bar', 
    'pass1' => 'foobar',
    'first_name' => 'Foo',
    'last_name' => 'Bar'
);

Register::signup($data);

if (Register::passes()) {
    // Successfully registered...
}  else {
    // There are some errors:
    print_r( Register::errors()->toArray() );
}
```

The `passes` method checks if the `$data` passes the validation and with the `errors` method you get the errors.

To display the errors much prettier you can do something like this:
    
```php
if (Register::fails()) {
    echo '<ul>';
    foreach (Register::errors()->all('<li>:message</li>') as $error) 
    {
       echo $error;
    }
    echo '</ul>';
}
```

If the signup is successful, the `auth.signup` event will be fired in `app/events.php`.

For a complete example see `code/versions/basic/singup.php` from the archive.

#### Activating Users

Once the user has been registered, if the `email_activation` option is enabled in `app/config/auth.php`, then an e-mail will be sent to the user with the activation reminder/link. The e-mail template for that email is located in `app/views/emails/activation.php`.

To activate the user use the the `Register::activate` method. 

```php
Register::activate($reminder);

if (Register::passes()) {
    // Account activated...
}
```

For a complete example see `activate.php`.

#### Resending Activation Reminder

To send the activation reminder/link again, use the `Register:reminder` method.

```php
Register::reminder($email);
                
if (Register::passes()) {
    // Activation sent...
}
```

For a complete example see `code/versions/basic/activation.php` from the archive.

See `src/Hazzard/Auth/Register.php` for the full list of methods and arguments.

## Password Reminders & Reset

#### Sending Password Reminder

To send the password reminder use the `Password:reminder` method.

```php
Password::reminder($email);

if (Password::passes()) {
    // Reminder sent...
}
```

The e-mail template for the password reminder is located in `app/views/emails/reminder.php`.

For a complete example see `code/versions/basic/reminder.php` from the archive.

#### Resetting Password

To reset the user password use the  `Password::reset` method. 

```php
Password::reset($password, $password_confirmation, $reminder);
            
if (Password::passes()) {
    // Password changed...
}
```

For a complete example see `code/versions/basic/reset.php` from the archive.

See `src/Hazzard/Auth/PasswordReminder.php` for the full list of methods and arguments.

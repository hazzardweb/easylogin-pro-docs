# User Meta
The User Meta allows to simply add, get, update and delete custom meta for the users.

#### Adding Metadata To A User

    Usermeta::add('user_id', 'meta_key', 'meta_value', true);

The last argument indicates whether the same key should not be added.

#### Retrieving Metadata For A User.
    $value = Usermeta::get('user_id', 'meta_key', true);

If the second argument is empty `''` all metadata for the user will be retrieved.
The last argument indicates whether to return a single value for the key.

#### Updating Metadata For A User.

    Usermeta::update('user_id', 'meta_key', 'meta_value');
    
#### Removing Metadata For A User.

    Usermeta::delete('user_id', 'meta_key');

If the second argument is omitted all metadata for the user will be removed.

See `src/Hazzard/User/Meta.php` for the full list of methods and arguments.
# Translation

- [Configuration](#configuration)
- [Language Files](#language-files)
- [Basic Usage](#basic-usage)

## Configuration

The language configuration is stored in `app/config/app.php` are:

`locale` - The default locale that will be used by the translation. Example: "en", "es", etc. <br>

`locales` - The available locales for translation. Example:

```php
'locales' => array(
    'en' => 'English', 
    'es' => 'Español',
),
```

## Language Files

Language strings are stored in files within the `app/lang` directory. Within this directory there should be a subdirectory for each language supported by your website.

```markup
/app
    /lang
        /en
            main.php
        /es
            main.php
```

## Basic Usage

#### Retrieving Lines From A Language File

```php
echo Lang::get('main.login');
// OR
echo trans('main.login');
// OR
_e('main.login'); // <=> echo trans('main.login');
```

The first segment of the string passed to the `get` method or `trans`/`_e` functions is the name of the language file, and the second is the name of the line that should be retrieved.

#### Making Replacements In Lines

You may also define place-holders in your language lines:
   
```php 
'welcome' => 'Howdy, :name !',
```
Then, pass a second argument of replacements to the `Lang::get` method or `trans`/`_e` functions:

```php
echo trans('main.welcome', array('name' => 'User'));
````

This will output: _Howdy, User !_

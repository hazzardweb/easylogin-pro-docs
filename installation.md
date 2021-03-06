# Installation

- [Server Requirements](#server-requirements)
- [Install EasyLogin Pro](#install-easylogin-pro)

## Server Requirements

- PHP >= 5.3.7 or >= 5.4 for the [mail api drivers](mail.md#api-drivers).
- MySQL >= 5.5.15
- PDO PHP Extension
- OpenSSL PHP Extension
- GD PHP Extension
- cURL PHP Extension
- Multibyte String PHP Extension
- Exif PHP Extension _(optional)_
- Internationalization _(optional)_

To make sure you have everything installed run `extra/php_check.php` in your browser to see the results.

## Install EasyLogin Pro

To install EasyLogin Pro simply follow the video tutorial or read the instructions below.

<p class="video-wrapper"><iframe allowfullscreen="1" frameborder="0" src="http://www.youtube.com/embed/ueqreubPzhg?rel=0&showinfo=0&vq=hd720"></iframe></p>

### 1. Extract files

Extract the files from the archive you have downloaded from CodeCanyon.

### 2. Copy files

Copy the files from the `code` directory to your server. <br> By default the script is set to the main example, but you can install the [other examples](installation.md#examples) too.

*Make sure the `uploads` directory has `0777` permission.

*For PHP < 5.4 copy and replace the contents from the `extra/php53-compat` to the root directory of the script.

### 3. Create a database & import the SQL file

Open a database client (phpMyAdmin, etc.), create a new database (and user) and import `database.sql` found in the `code` directory or in the one you copied earlier.

### 4. Configuration

First edit `app/config/database.php` and set the database connection details.

Then edit `app/config/app/php` and set `url` to the url where the script is located. For example if you have copied the script files into a directory called "elp" and your website is "http://mywebsite.com" then the `url` should be set to "http://mywebsite.com/elp". <br>
Set the `key` to a random 32 character string. Click <a href="javascript:generateKey()">here</a> to generate a random key.

<b id="key"></b>

Make sure to set the permissions to `775` (recursively) for  `app/storage`.

Now you can open the script in your browser.
To log in use the username `admin` and password `admin`. <br>
*Make sure you change the password after you log in the first time.

Next you should continue with the [Configuration](configuration.md) and [Social Authentication](social-auth.md) sections.

## Other Examples

If you want to use other examples than the main one copy the files from the example directory you want (basic, basic-ajax, inline or modal) from `extra/examples` to the main directory. Replace if necessary.

There are few tweaks you have to make for these examples:

#### basic, basic-ajax and inline:

Edit `app/views/comments.php`, find this line

```php
<!-- <?php _e('comments.logged_in', array('attrs' => 'href="login.php"')) ?> -->
```

remove the comments (`<!--` and `-->`), and make sure you comment the next line.

Then edit `app/views/header.php` find these lines:

```php
<!--
<li><a href="login.php"><?php _e('main.login'); ?></a></li>
<li><a href="signup.php"><?php _e('main.signup'); ?></a></li>
-->
```

and again remove the comments (`<!--` and `-->`) (and make sure you comment the next lines)

This will change the links to separate pages instead of using a modals.

#### modal:

Edit `app/views/emails/activation.php` and uncomment this line:

```php
// $url = App::url("#activate-{$reminder}");
```

Edit `app/views/emails/reminder.php` and uncomment this line:

```php
// $url = App::url("#reset-{$reminder}");
```

This will change activation and password reminder the links to modals.

<script>
    function generateKey() {
        var key  = '',
            pool = '0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ';

        for (var i = 32; i > 0; --i) {
            key += pool[Math.round(Math.random() * (pool.length - 1))];
        }

        document.getElementById('key').innerText = key;
    }
</script>

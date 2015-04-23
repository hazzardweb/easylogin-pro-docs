# Configuration

- [General](#general)
- [Mail](#mail)
- [Captcha](#captcha)
- [Authentication](#authentication)
- [Private Messages](#private-messages)
- [Comments](#comments)
- [Enable Admin Configuration](#enable-admin-configuration)
- [PHP < 5.3.7 Basic Hasher](#php-<-5.3.7-basic-hasher)

## General

The general options for the script are stored in `app/config/app.php`. 

You can change the script debug mode, url, name, color scheme, language, timezone, encryption key, etc.

Notes:

The `url` is the url to the script files. For example if your website is "http://mywebsite.com" and you have copied the script file in the root directory, then the `url` will be the same as the website url. But if you have the script files into another directory, "elp", then the `url` will be "http://mywebsite.com/elp". Try to avoid using "www" in the url because the AJAX may not work.

The `key` is used to encrypt the cookies in the browser. This should be set to a random 32 character string. Use `extra/generate_key.php` to generate a key.

## Mail

See the [Mail](mail.md) section.

## Captcha

It's highly recommended to use captcha for preventing spam.

<p class="video-wrapper"><iframe allowfullscreen="1" frameborder="0" src="http://www.youtube.com/embed/xe-xYmbUFls?rel=0&showinfo=0&vq=hd720"></iframe></p>

To enable Captcha first set the `captcha` option to `true` in  `app/config/auth.php`. Next, visit <a href="https://www.google.com/recaptcha/admin" target="_blank">reCAPTCHA</a>, click on the __Sign up Now__ button, enter your Domain and click __Register__.

Once created click on the domain name and copy the __Site Key__ and __Secret Key__ to  `app/config/services.php` under the `recaptcha` section like this:

    'recaptcha' => array(
        'public_key'  => 'your-site-key',
        'private_key' => 'your-secret-key'
    ),

## Authentication
The options for Authentication are stored in `app/config/auth.php`.

You can set if you want users to have a username, allow them to change the username, allow to delete their account, send email activation links, set the default role ID, enable captcha, set the login redirect url and set the [Social Authentication](social-auth.md) providers.

Notes:

The `default_role_id` must be the role ID that you want the new user to have when they sign up.

If you enable `email_activation` make sure you have set the an [e-mail](mail.md).

## Private Messages

The options for Private Messages are stored in `app/config/pms.php`. The options allow you enable/disable the realtime feature, change the messages maxlength, limit and the website webmaster.
The `webmaster` must be set to the ID of the admin. By default is set `1`, the ID of the admin account created by the script.

## Comments
The options for Comments are stored in `app/config/comments.php`. The options allow you to enable manual moderation, add restricted works, add blacklisted/whitelisted users, set how many comments you want to display per page, enable smilies* and other settings.

*If you enable smilies for the comments you have to also define the smilies images in `app/config/smilies.php`.  By default the script does not have the actual images included. You can use your own images or buy [these](http://graphicriver.net/item/matte-motes-emoticon-set/33923).

## Enable Admin Configuration

EasyLogin Pro allows you to change the script options without having to edit the config files. However this may affect the performance of your website.

To enable, open `app/init.php` and search for _Database Config Loader_, then uncomment the these lines:

    $app->register('Hazzard\Database\DatabaseServiceProvider');
    $loader->setConnection($app['db']);
    $app->instance('config', new Config($loader));

Now if you go to the Admin Panel `admin.php` you'll see a new section for Settings. Please note that in this documentation everything is referred to the file configuration, but since the name of the options are similar, there should not be a problem when changing the configuration from the Admin Panel. 

Even if you enable this feature, the script will still look for the configuration options in the configuration files if the options does not exists in the database, basically will merge them.

Also not all configuration options will be available in the Admin Panel for obvious reasons.

## PHP < 5.3.7 Basic Hasher

First of all if you have PHP < `5.3.7` you should consider upgrading. However, if that's not an option for you, you can disable the `bcrypt` password hashing and enable `md5`.

Edit `src/Hazzard/Hashing/HashServiceProvider.php` and in the `register` method comment the first part and uncomment the last one like this:

    public function register()
    {
        //$this->app->bindShared('hash', function($app) {
        //    return new BcryptHasher;
        //});

        // Use this if you don't have BCRYPT on your server.
        $this->app->bindShared('hash', function($app) {
            // "md5", "sha256", "haval160,4" etc.
            return new BasicHasher('md5');
        });
    }

>The `md5` password hasher is considered to be the weakest one. Use it at your own risks. 

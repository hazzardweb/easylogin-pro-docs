# Mail

- [Configuration](#configuration)
- [Templates](#templates)
- [Basic Usage](#basic-usage)

## Configuration

The mail configuration file is `app/config/mail.php`, and contains options allowing you to change your SMTP host, port, and credentials, as well as the `from` address. If you wish to use the PHP `mail` function or `sendmail` you may change the `driver` in the configuration file.

### SMTP Example

```php
'driver' => 'smtp',
'host' => 'mail.example.com',
'port' => 587,
'from' => array('address' => 'mail@example.com', 'name' => 'My Website'),
'encryption' => 'tls',
'username' => 'mail@example.com',
'password' => 'mail-password',
```

### Gmail Example

If you don't have an e-mail on your server you can even use a Gmail account.

```php
'driver' => 'smtp',
'host' => 'smtp.gmail.com',
'port' => 587,
'from' => array('address' => 'your-gmail-address@gmail.com', 'name' => 'My Website'),
'encryption' => 'tls',
'username' => 'your-gmail-address@gmail.com',
'password' => 'your-gmail-password',
```

### API Drivers

There [Mailgun](https://www.mailgun.com), [Mandrill](https://www.mandrill.com) and [SparkPost](https://www.sparkpost.com) api drivers require PHP >= `5.4`.

#### Mailgun

Copy your [Mailgun](https://www.mailgun.com) __API Key__ and __Domain__ to `app/config/services.php` under the `mailgun` section:

```php
'mailgun' => array(
    'secret' => 'your-mailgun-key',
    'domain' => 'your-mailgun-domain'
),
```

#### Mandrill

Copy your [Mandrill](https://www.mandrill.com) __API Key__ to `app/config/services.php` under the `mandrill` section:

```php
'mandrill' => array(
    'secret' => 'your-mandrill-key',
),
```

#### SparkPost

Copy your [SparkPost](https://www.sparkpost.com) __API Key__ to `app/config/services.php` under the `sparkpost` section:

```php
'sparkpost' => array(
    'secret' => 'your-sparkpost-key',
),
```

## Templates

The e-mail templates are stored in `app/views/emails/`. These are used when sending the activation e-mail, the password reminder, etc.

## Basic Usage

If you want to send your custom e-mails you can use `Mail::send` method:
 
```php
$data = array('body' => 'Welcome to My Website!');

Mail::send('emails.welcome', $data, function($message) {
    $message->to('foo@example.com', 'John Doe');
    $message->subject('Welcome!');
});
```

The first argument passed to the `send` method is the name of the view (app/views/emails/welcome.php) that should be used as the e-mail body. The second is the `$data` that should be passed to the view, and the third is a Closure allowing you to specify various options on the e-mail message.

For all the methods available on the `$message` instance please see `src/Hazzard/Mail/Message.php`.

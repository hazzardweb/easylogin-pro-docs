# Mail

- [Configuration](#configuration)
- [Templates](#templates)
- [Basic Usage](#basic-usage)

## Configuration

The mail configuration file is `app/config/mail.php`, and contains options allowing you to change your SMTP host, port, and credentials, as well as the `from` address. If you wish to use the PHP `mail` function or `sendmail` you may change the `driver` in the configuration file.

### SMTP Example

    'driver' => 'smtp',
    'host' => 'mail.example.com',
    'port' => 587,
    'from' => array('address' => 'mail@example.com', 'name' => 'My Website'),
    'encryption' => 'tls',
    'username' => 'mail@example.com',
    'password' => 'mail-password',

### Gmail Example

If you don't have an e-mail on your server you can even use a Gmail account.

    'driver' => 'smtp',
    'host' => 'smtp.gmail.com',
    'port' => 587,
    'from' => array('address' => 'my-gmail-address@gmail.com', 'name' => 'My Website'),
    'encryption' => 'tls',
    'username' => 'my-gmail-address@gmail.com',
    'password' => 'my-gmail-password',

### API Drivers

There are included drivers for the <a href="http://www.mailgun.com/" target="_blank">Mailgun</a> and <a href="https://www.mandrill.com/">Mandrill</a>. Both drivers require PHP>=`5.4`. 
First you have to install them by copying the contents from the  `extra/mailgun-mandrill-api` directory to the root directory of the script. Next, follow the instructions for each one.

#### Mailgun

To use the Mailgun driver, set the `driver` option to `mailgun` in `app/config/mail.php`. Next, go to the <a href="https://mailgun.com/cp" target="_blank">Mailgun CP</a>, click on the __Add Your Domain__ button and add your website domain name.

Once created go back to the __Mailgun CP__ and copy the __API Key__ and the domain you just created to `app/config/services.php` under the `mailgun` section like this:

    'mailgun' => array(
        'secret' => 'your-mailgun-key',
        'domain' => 'your-mailgun-domain'
    ),

#### Mandrill

To use the Mandrill driver, set the `driver` option to `mandrill` in `app/config/mail.php`. Next, go to the <a href="https://mandrillapp.com" target="_blank">Mandrill App</a>, click on the __Get API Keys__ button then on the __+ Add API Key__ button.

Once created copy the __API Key__ to `app/config/services.php` under the `mandrill` section like this:

    'mandrill' => array(
        'secret' => 'your-mandrill-key',
    ),

## Templates

The e-mail templates are stored in `app/views/emails/`. These are used when sending the activation e-mail, the password reminder, etc.

## Basic Usage

If you want to send your custom e-mails you can use `Mail::send` method:
    
    $data = array('body' => 'Welcome to My Website!');
    Mail::send('emails.welcome', $data, function($message) {
        $message->to('foo@example.com', 'John Doe');
        $message->subject('Welcome!');
    });

The first argument passed to the `send` method is the name of the view (app/views/emails/welcome.php) that should be used as the e-mail body. The second is the `$data` that should be passed to the view, and the third is a Closure allowing you to specify various options on the e-mail message.

For all the methods available on the `$message` instance please see `src/Hazzard/Mail/Message.php`.

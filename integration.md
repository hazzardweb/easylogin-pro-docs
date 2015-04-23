# Integration

- [Basic Integration](#basic)
- [Ajax Integration](#ajax)

Beside the main example, EasyLogin Pro can be easily integrated in your already existing website. You have to include some files and then use the available methods to make the log in, sign up etc. work.

<a name="basic"></a>
## [Basic Integration](#basic)

The basic integration is fairly easy. First inlcude `app/init.php` in your existing website, make sure you include the file before the `<html>` tag, otherwise some errors may occur.

    require_once 'app/init.php';

Now you can access the classes and functions from EasyLogin Pro, like the [Authentication](/docs/auth).

#### Log In Form Example

    <?php require_once 'app/init.php'; ?>
    <?php
        if (isset($_POST['submit']) && csrf_filter()) {
            Auth::login($_POST['email'], $_POST['password'], isset($_POST['remember']));
            
            if (Auth::passes()) redirect_to('index.php');
        }
    ?>
    <html>
        <head></head>
        <body>
            <?php 
                if (Auth::fails()) {
                    echo '<ul>';
                    foreach (Auth::errors()->all('<li>:message</li>') as $error) {
                       echo $error;
                    }
                    echo '</ul>';
                }
            ?>
            <form action="" method="POST">
                <?php csrf_input() ?>
                <input type="text" name="email" placeholder="Email or Username"><br>
                <input type="password" name="password" placeholder="Password"><br>
                <button type="submit" name="submit">Log in</button>
            </form>
        </body>
    </html>

`<?php csrf_input() ?>` will add a hidden input with a token and the `csrf_filter()` function will check if the token is valid. This is used against CSRF attacks.

See the complete example in `extra/examples/basic/login.php` as well as others.

<a name="ajax"></a>
## [Ajax Integration](#ajax)

For the ajax integration there are few more things to be considered.

First inlcude `app/init.php` in your existing website, make sure you include the file before the `<html>` tag, otherwise some errors may occur.

    require_once 'app/init.php';

Next, include the JavaScript files, as well as the `csrf meta` inside the `<head>` tag:
    
    <meta name="csrf-token" content="<?php echo csrf_token() ?>">
    <script src="assets/js/vendor/jquery-1.11.1.min.js"></script>
    <script src="assets/js/vendor/bootstrap.min.js"></script>
    <script src="assets/js/easylogin.js"></script>
    <script src="assets/js/main.js"></script>
    <script>
        EasyLogin.options = {
            ajaxUrl: '<?php echo App::url("ajax.php") ?>',
            lang: <?php echo json_encode(trans('main.js')) ?>,
            debug: <?php echo Config::get('app.debug') ?>,
        };
    </script>

The `csrf meta` can be omitted if you disable `csrf` in `app/config/app.php`.

Now for each form add the `.ajax-form` class and set the `action` attribute to the action you want ("login", "singup", etc.). 

#### Log In Form Example

    <?php require_once 'app/init.php'; ?>
    <html>
        <head>
            <meta name="csrf-token" content="<?php echo csrf_token() ?>">
            <script src="assets/js/vendor/jquery-1.11.1.min.js"></script>
            <script src="assets/js/vendor/bootstrap.min.js"></script>
            <script src="assets/js/easylogin.js"></script>
            <script src="assets/js/main.js"></script>
            <script>
                EasyLogin.options = {
                    ajaxUrl: '<?php echo App::url("ajax.php") ?>',
                    lang: <?php echo json_encode(trans('main.js')) ?>,
                    debug: <?php echo Config::get('app.debug') ?>,
                };
            </script>
        </head>
        <body>
            <form action="login" class="ajax-form">
                <input type="text" name="email" placeholder="Email or Username"><br>
                <input type="password" name="password" placeholder="Password"><br>
                <button type="submit" name="submit">Log in</button>
            </form>
        </body>
    </html>

When you submit the form, an ajax request will be sent to `ajax.php` and the `login` action (or whatever value does the `action` attribute have) will be executed.

See the complete example in extra/examples/basic-ajax/login.php as well as others.
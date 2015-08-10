# Basic Integration

- [Log in](#log-in)
- [Sign up](#sign-up)

Before continue make sure when you installed the script you have copied the files from `extra/examples/basic`.

The basic version allows you add all the functionality of the script into your website using your own design and forms. The script provides just a set of classes and methods for you to do that.

## Log in

```php
<?php
// Init file
require_once 'app/init.php';

// Check if is already logged in
if (Auth::check()) redirect_to(App::url());

// Form submit
if (isset($_POST['submit']) && csrf_filter()) {
    Auth::login($_POST['email'], $_POST['password'], isset($_POST['remember']));

    if (Auth::passes()) {
        $url = Config::get('auth.login_redirect');
        $url = empty($url) ? App::url() : $url;
        redirect_to($url);
    }
}
?>
<html>
<head></head>
<body>
    <h3><?php _e('main.login') ?></h3>
    <!-- Show log in errors -->
    <?php if (Auth::fails()) {
        echo '<ul>';
        foreach (Auth::errors()->all('<li>:message</li>') as $error) {
           echo $error;
        }
        echo '</ul>';
    } ?>
    <form action="" method="POST">
        <?php csrf_input() ?> <!-- Security input -->
        <p>
            <label for="email"><?php _e('main.email_username') ?></label>
            <input type="text" name="email" id="email" value="<?php echo set_value('email') ?>">
        </p>
        <p>
            <label for="password"><?php _e('main.password') ?></label>
            <input type="password" name="password" id="password">
        </p>
        <p>
            <label><input type="checkbox" name="remember" value="1"> <?php _e('main.remember') ?></label>
        </p>
        <p>
            <button type="submit" name="submit"><?php _e('main.login') ?></button>
        </p>
        <p>
            <a href="reminder.php"><?php _e('main.forgot_pass') ?></a> <br>
            <a href="activation.php"><?php _e('main.resend_activation') ?></a>
        </p>
    </form>
    <!-- Show social auth -->
    <?php if (count(Config::get('auth.providers'))): ?>
        <p><?php _e('main.login_with2') ?></p>
        <p>
            <?php foreach (Config::get('auth.providers', array()) as $key => $provider): ?>
                <a href="<?php echo App::url("oauth.php?provider={$key}") ?>"><?php echo $provider ?></a>
            <?php endforeach ?>
        </p>
    <?php endif ?>
</body>
</html>
```

Source: `extra/examples/basic/login.php`.

## Sign up

```php
<?php
require_once 'app/init.php';

if (Auth::check()) redirect_to(App::url());

if (isset($_POST['submit']) && csrf_filter()) {
    Register::signup($_POST);

    if (Register::passes()) {
        if (Config::get('auth.email_activation')) {
            redirect_to('signup.php', array('signup_complete' => true));
        } else {
            Auth::login($_POST['email'], $_POST['pass1']);

            $redirect = Config::get('auth.login_redirect');
            redirect_to($redirect != '' ? $redirect : App::url());
        }
    }
}
?>
<html>
<head></head>
<body>
    <?php if (Session::has('signup_complete')): Session::deleteFlash(); ?>
        <h3><?php _e('main.check_email') ?></h3>
        <?php _e('main.activation_check_email') ?>
    <?php else: ?>
        <h3><?php _e('main.signup') ?></h3>
        <!-- Show register errors -->
        <?php if (Register::fails()) {
            echo '<ul>';
            foreach (Register::errors()->all('<li>:message</li>') as $error) {
               echo $error;
            }
            echo '</ul>';
        } ?>
        <form action="" method="POST">
            <?php csrf_input() ?>
            <?php if (Config::get('auth.require_username')): ?>
                <p>
                    <label for="signup-username"><?php _e('main.username') ?></label>
                    <input type="text" name="username" id="signup-username" value="<?php echo set_value('username') ?>">
                </p>
            <?php endif ?>
            <p>
                <label for="signup-email"><?php _e('main.email') ?></label>
                <input type="text" name="email" id="signup-email" value="<?php echo set_value('email') ?>">
            </p>
            <p>
                <label for="signup-pass1"><?php _e('main.password') ?></label>
                <input type="password" name="pass1" id="signup-pass1" autocomplete="off" value="">
            </p>
            <!-- Custom fields required for signup -->
            <?php echo UserFields::build('signup') ?>
            <!-- Show captcha if enabled -->
            <?php if (Config::get('auth.captcha')): ?>
                <p class="recaptcha">
                    <label for="recaptcha_response_field"><?php _e('main.enter_captcha') ?></label>
                    <div id="recaptcha_widget" class="recaptcha-outer" style="display:none">
                        <div id="recaptcha_image" class="recaptcha-image"></div>
                        <div class="recaptcha-controls">
                            <div><a href="javascript:Recaptcha.reload()" tabindex="-1"><?php _e('main.captcha_reload') ?></a> |</div>
                            <div class="recaptcha_only_if_image"><a href="javascript:Recaptcha.switch_type('audio')" tabindex="-1"><?php _e('main.captcha_listen') ?></a> |</div>
                            <div class="recaptcha_only_if_audio"><a href="javascript:Recaptcha.switch_type('image')" tabindex="-1"><?php _e('main.captcha_image') ?></a> |</div>
                            <div><a href="javascript:Recaptcha.showhelp()" tabindex="-1"><?php _e('main.captcha_help') ?></a></div>
                        </div>
                        <input type="text" name="captcha" id="recaptcha_response_field">
                    </div>
                    <script type="text/javascript">
                        var RecaptchaOptions = {
                            theme : 'custom',
                            custom_theme_widget: 'recaptcha_widget'
                        };
                     </script>
                    <script src="https://www.google.com/recaptcha/api/challenge?k=<?php echo Config::get('services.recaptcha.public_key') ?>"></script>
                </p>
            <?php endif ?>
            <p>
                <button type="submit" name="submit"><?php _e('main.signup') ?></button>
            </p>
        </form>
        <!-- Show social auth -->
        <?php if (count(Config::get('auth.providers'))): ?>
            <p><?php _e('main.login_with2') ?></p>
            <p>
                <?php foreach (Config::get('auth.providers', array()) as $key => $provider): ?>
                    <a href="<?php echo App::url("oauth.php?provider={$key}") ?>"><?php echo $provider ?></a>
                <?php endforeach ?>
            </p>
        <?php endif ?>
    <?php endif ?>
</body>
</html>
```

Source: `extra/examples/basic/signup.php`.

# Modal Integration

Before continue make sure when you installed the script you have copied the files from `extra/examples/modal`.

The modal version allows you to integrate the script into your existing website without having to worry about that the CSS from the models will conflict with your own CSS.

   First inlcude `app/init.php` in your existing website, make sure you include the file before the `<html>` tag, otherwise some errors may occur.

    <?php require_once 'app/init.php'; ?>

Now include the CSS and JavaScript files and add the buttons for log in, sign up, log out, messages, admin, etc. 

    <?php require_once 'app/init.php'; ?>
    <html>
    <head>
        <!-- CSRF Token -->
        <meta name="csrf-token" content="<?php echo csrf_token() ?>">
        
        <!-- Bootstrap and some custom CSS  -->
        <link href="<?php echo asset_url('css/vendor/bootstrap-noconflict.min.css') ?>" rel="stylesheet">
        <link href="<?php echo asset_url('css/modal-only.css') ?>" rel="stylesheet">
        
        <!-- JavaScript -->
        <script src="<?php echo asset_url('js/vendor/jquery-1.11.1.min.js') ?>"></script>
        <script src="<?php echo asset_url('js/vendor/bootstrap.min.js') ?>"></script>
        <script src="<?php echo asset_url('js/easylogin.js') ?>"></script>
        <script src="<?php echo asset_url('js/main.js') ?>"></script>
        <script>
            EasyLogin.options = {
                ajaxUrl: '<?php echo App::url("ajax.php") ?>',
                lang: <?php echo json_encode(trans('main.js')) ?>,
                debug: <?php echo Config::get('app.debug')?1:0; ?>,
            };
        </script>
    </head>
    <body>
        <?php if (Auth::guest()): ?>
            <!-- Show Login and Sigup buttons -->
            <p>
                <a href="#" data-toggle="modal" data-target="#loginModal">Log in</a> |
                <a href="#" data-toggle="modal" data-target="#signupModal">Sign up</a>
            </p>
        <?php else: ?>
            <!-- Show user name, avatar and some links -->
            <p>Howdy, <a href="profile.php?u=<?php echo Auth::user()->id ?>"><?php echo Auth::user()->display_name; ?></a></p>
            <p><img src="<?php echo Auth::user()->avatar ?>" width="50"></p>
            <p>
                <a href="#" data-toggle="modal" data-target="#settingsModal">Settings</a> |
                <a href="javascript:EasyLogin.openPMS()">Messages</a> <span class="pm-notification" style="padding:0"></span> |
                <?php if (Auth::userCan('dashboard')): ?><a href="admin.php">Admin</a> |<?php endif ?>
                <a href="javascript:EasyLogin.logout()">Log out</a>
            </p>
        <?php endif ?>

        <?php echo View::make('modals.load'); ?>
    </body>
    </html>
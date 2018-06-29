# Upgrade Guide

- [Git Changes](#git-changes)
- [Upgrading To 1.3.3](#upgrading-to-133)
- [Upgrading To 1.3.2](#upgrading-to-132)
- [Upgrading To 1.3.1](#upgrading-to-131)
- [Upgrading To 1.3.0](#upgrading-to-130)
- [Upgrading To 1.2.11](#upgrading-to-1211)
- [Upgrading To 1.2.10](#upgrading-to-1210)
- [Upgrading To 1.2.9](#upgrading-to-129)
- [Upgrading To 1.2.8](#upgrading-to-128)
- [Upgrading To 1.2.7](#upgrading-to-127)
- [Upgrading To 1.2.6](#upgrading-to-126)
- [Upgrading To 1.2.5](#upgrading-to-125)
- [Upgrading To 1.2.4](#upgrading-to-124)
- [Upgrading To 1.2.3](#upgrading-to-123)
- [Upgrading To 1.2](#upgrading-to-12)
- [Upgrading To 1.1](#upgrading-to-11)

## Git Changes

You can view the all the changes on [git.hazzardweb.com](http://git.hazzardweb.com).

## Upgrading To 1.3.3

- Replace `oauth.php`
- Replace `src/Hazzard/Support/Recaptcha.php`
- Replace `assets/js/vendor/jquery.imgpicker.js`

## Upgrading To 1.3.2

Replace the `vendor` directory.

## Upgrading To 1.3.1

Replace the `vendor` directory.

## Upgrading To 1.3.0

#### Updating Dependencies

- Replace `vendor` and `composer.json`
- For PHP < 5.4 copy and replace the contents from the `extra/php53-compat` to the root directory of the script

#### Encryption

- Replace `src/Hazzard/Encryption` and `app/init.php`

#### Mail

- Replace `src/Hazzard/Mail`, `app/views/admin/options-services.php` and `app/views/admin/options-mail.php`
- Add `'sparkpost' => array('secret' => ''),` in `app/config/services.php`

#### Exception Handler

- Replace `src/Hazzard/Exception/Handler.php` and `app/init.php`

#### Comments

- Delete `app/config/smiles.php`
- Replace `app/views/comments.php`
- Add `src/Hazzard/Formatting` directory
- Replace `src/Hazzard/Comments/Comments.php`
- Replace `assets/js/comments.js` and `assets/css/comments.css`

#### OAuth

Only if you want to add Spotify as an oauth provider.

- Add `src/OAuth/UserData/Extractor/Spotify.php`
- Add `.connect.spotify{background: #2ebd59;}` in `assets/css/main.css`
- Add `'spotify' => array('user-read-email', 'user-read-birthdate'),` in `oauth.php` under `$scopes`
- Add `'spotify' => array('id' => '', 'secret' => ''),` in `app/config/services.php`
- Add `// 'spotify' => 'Spotify',` in `app/config/auth.php` under the `providers` array

#### Database

- Replace `src/Hazzard/Database/Query.php`
- In `app/config/database.php` change `charset` to `utf8mb4` and `collation` to `utf8mb4_unicode_ci`

To enable `utf8mb4` for your old database dump your tables and data into a `.sql` file then edit it and replace `CHARSET=utf8` with `CHARSET=utf8mb4`.

Now run `ALTER DATABASE your_database_name CHARACTER SET = utf8mb4 COLLATE = utf8mb4_unicode_ci;` to convert the database and import back the `.sql` file.

Alternatively, you can follow [this guide](https://mathiasbynens.be/notes/mysql-utf8mb4) and only change the charset for the tables and collumns you want.

#### Misc

- Replace `src/Hazzard/Support/Str.php`
- Replace `src/Hazzard/Support/ImagePicker.php`
- Replace `src/Hazzard/Validation/Validator.php`

## Upgrading To 1.2.11

- Copy `extra/facebook-fix/Facebook.php` to `vendor/lusitanian/oauth/src/OAuth/OAuth2/Service`.
- Replace `src/Hazzard/Support/helpers.php @ csrf_filter`
- PHP 7.1 only: replace `error_reporting(-1);` with `error_reporting(E_ALL & ~E_DEPRECATED);` in `app/init.php`.

## Upgrading To 1.2.10

- Replace `src/OAuth/UserData/Extractor/Facebook.php`. This is only required if your Facebook app is >= 2.8.

## Upgrading To 1.2.9

- Replace `oauth.php`
- Replace `app/views/admin/users.php`
- Replace `src/OAuth/UserData/Extractor/Twitter.php`
- Replace `src/Hazzard/User/Fields.php` and `FieldsServiceProvider.php`

## Upgrading To 1.2.8

- Replace `ajax.php@ajax_send_message`
- Replace `extra/linkedin/index.php`
- Add `src/Hazzard/Database/Expression.php`
- Replace `src/Hazzard/Database/Connection.php` and `Query.php`

## Upgrading To 1.2.7

- Replace `ajax.php`
- Replace `src/Hazzard/Support/helpers.php`
- Replace `src/Hazzard/Support/Recaptcha.php`
- Replace `src/Hazzard/Support/DataTables.php`
- Replace `src/Hazzard\Messages/Message.php`
- Replace `assets/js/main.js`
- Replace `assets/js/easylogin.js`
- If you are using the versions with JavaScript (default, inline or basic-ajax), replace `display_captcha()` with `display_captcha_tag()` in `signup.php`, `activation.php` and `reminder.php`.

## Upgrading To 1.2.6

- Replace `src/Hazzard/Support/DataTables.php`

## Upgrading To 1.2.5

- Replace `ajax.php` (`ajax_avatar` function)
- Replace `assets/js/vendor/jquery.imagepicker.js`
- Replace `src/Hazzard/Support/ImagePicker.php`

## Upgrading To 1.2.4

- Replace `app/models/Comment.php` (`toArray` method)
- Replace `src/Hazzard/Support/helpers.php` (`mb_substr` function)
- Replace `app/models/User.php`
- Replace `app/views/modals/settings.php`
- Replace `assets/css/comments.css` (`.comment-text`)
- Replace `src/Hazzard/Database/Query.php` (`compileOrders` method)

## Upgrading To 1.2.3

This update brings some OAuth fixes for Facebook and Linkedin as well as few other minor fixes and tweaks.

Visit [git.hazzardweb.com](http://git.hazzardweb.com) and browse the `easylogin-pro` repository's commits to see the extact changes (starting from May 16, 2015).

- Replace `app/models/User.php` (or just the `generateAvatar` method).
- Replace `ajax.php` (or just the `ajax_avatar` function).
- Replace `oauth.php`. If you are using Linkedin you need to [install](social-auth.md#linkedin) it again.
- Replace the `src/OAuth` directory.
- (Optional) Replace the `vendor` directory. If you are using Mailgun or Mandrill [install](mail.md#api-drivers) the API drivers again.

## Upgrading To 1.2

The `1.2` upgrade consists mostly in some bug fixes (nothing related to security) and cleaning up few things. It also brings the new reCAPTCHA and few things here and there.

Since there are a lot of small changes a lot of files if you want to upgrade from `1.1.4` you'll have to go to [git.hazzardweb.com](http://git.hazzardweb.com), log in with your Purchase Code from CodeCanyon and then go to the __Commits__ tab scroll down, click on the __Older__ button until you find this commit *Fixed comment moderation option* made on 13/01/2015 21:52:23. From there go up and see what files have changed and change yours too. Also make sure to replace the `vendor` directory because all packages have been updated.

## Upgrading To 1.1

The `1.1` update brings the comment system, some bug fixes (mostly for PHP<5.4) and some other changes. <br> If you don't want the comment system and you don't have any issues you don't have to upgrade.

Recommended would be to a fresh install, but if that's not the case follow these steps:

- Edit `app/config/app.php` and add `'Hazzard\Comments\CommentsServiceProvider'` to the `providers` array and `'Comments'   => 'Hazzard\Support\Facades\Comments',` to the `aliases` array.
- Add `app/config/comments.php` and `app/config/smilies.php`
- Replace `app/lang/en` (or replace only the necessary lines)
- Replace `app/models/User.php`
- Add `app/models/Comment.php` and `app/models/CommentVote.php`
- Delete `app/storage/services.json`
- Replace `app/views` (or only replace `header.php`, `footer.php`, `modals/load.php`, `modals/settings.php` and add `comments.php`)
- Replace `app/events.php`
- Replace `assets/css` (or only replace `pms.css`, `main.css`, `bootstrap-custom.css`, `admin.css` and add `modal-only.css`, `comments.css`, `vendor/bootstrap-noconflict.min.css`)
- Replace `assets/js` (or only replace `main.js`, `admin.js`, `vendor/jquery.imgpicker.js` and add `comments.js`, `embed-comments.js`, `vendor/iframeResizer.contentWindow.min.js`, `vendor/iframeResizer.min.js`)
- If you have used anything from `extra` replace as well.
- Import `extra/comments.sql`
- Add `comments.php` and `embed-comments.php`
- Replace `ajax.php`, `settings.php`
- Replace `src/ImagePicker/ImgPicker.php`
- Replace `src/Hazzard` (or only replace `Auth`, `Database/Query.php`, `Database/Model.php`, `Support/DataTables.php`, `Support/helpers.php`, `Validation/ValidationServiceProvider.php` and add `Comments`, `Support/Facades/Comments.php`, `Support/Kses.php`)

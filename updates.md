# Updates

- [Git](#git)
- [Upgrading To 1.2 From 1.1](#upgrading-to-12-from-11)
- [Upgrading To 1.1 From 1.0](#upgrading-to-11-from-10)

## Git

Each update for EasyLogin Pro will be available on CodeCanyon. However if you want to get the latest changes, before the update hits CodeCanyon, compare the versions and see exactly what files were changed, we have created a GitHub like app,  [git.hazzardweb.net](http://git.hazzardweb.net/).

When you go there you'll be asked for a __Purchase Code__. This code can be found in your <a href="http://codecanyon.net/downloads" target="_blank">Downloads</a> list on CodeCanyon. Once you have the code you can log in.

<a href="http://i.imgur.com/wiMdI1W.png" target="_blank"><img src="http://i.imgur.com/wiMdI1W.png" width="400"></a>

If you have any questions use the contact form on CodeCanyon or the e-mail <a href="mailto:hazzardweb@gmail.com" target="_blank">hazzardweb@gmail.com</a>.

## Upgrading To 1.2 From 1.1

The full list of changes can be found here on [git.hazzardweb.net](http://git.hazzardweb.net/).

The `1.2` upgrade consists mostly in some bug fixes (nothing related to security) and cleaning up few things. It also brings the new reCAPTCHA and few things here and there. 

Since there are a lot of small changes a lot of files if you want to upgrade from `1.1.4` you'll have to go to [git.hazzardweb.net](http://git.hazzardweb.net), log in with your Purchase Code from CodeCanyon and then go to the __Commits__ tab scroll down, click on the __Older__ button until you find this commit *Fixed comment moderation option* made on 13/01/2015 21:52:23. From there go up and see what files have changed and change yours too. Also make sure to replace the `vendor` directory because all packages have been updated.
  
## Upgrading To 1.1 From 1.0

The full list of changes can be found here on [git.hazzardweb.net](http://git.hazzardweb.net/).

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

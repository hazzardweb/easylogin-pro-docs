# Debugging

- [Ajax Errors](#ajax-errors)
- [Error Handling](#error-handling)

To enable error reporting make sure the `debug` mode is set to `true` in `app/config/app.php`. <br> Also make sure you have the errors turned on in your PHP config file (php.ini).

## Ajax Errors

If you came across an error like "_Oops! Something went wrong._", check your browser's __Console__ and __Network__ tabs for more information.

<p class="video-wrapper"><iframe src="https://www.screenr.com/embed/27ON" width="650" height="396" frameborder="0"></iframe></p>

If you get errors about the "Request Origin" request make sure you accept the request in `ajax.php` from where you send it by adding:

    header('Access-Control-Allow-Origin: yourwebsite.com');
    header('Access-Control-Allow-Origin: www.yourwebsite.com');

## Error Handling

EasyLogin Pro comes with a <a href="https://github.com/filp/whoops" target="_blank">whoops</a> error handling. However, if you want to disable it open `app/init.php` search for "_Register Custom Exception Handling_" and delete/comment this line:

    $app->startExceptionHandling();

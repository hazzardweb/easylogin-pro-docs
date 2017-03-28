# Release Notes

## v1.2.11 - 2017-03-28

- Fixed Facebook OAauth.
- Fixed csrf_filter helper.
- Fixed csrf check.
- Fixed deprecation error.

## v1.2.10 - 2016-12-18

- Fixed deprecated Facebook field.

## v1.2.9 - 2016-06-27

- Fixed LinkedIn disconnect redirect
- Fixed Twitter avatar url to use https
- Fixed admin users table when username is disabled
- Added `role_id` option to the [User Fields](userfields.md) that allows to specify the role id (or array of role ids) for which the field is displayed

## v1.2.8 - 2016-06-15

- Fixed email body when sending a message (`ajax.php@ajax_send_message`)
- [MySQL 5.6.2x] Change the default value of the `updated` column (`database.sql`)
- [MySQL 5.6.2x] Make password null by default (`database.sql`)
- Added [DB::groupBy](queries.md#order-by,-group-by,-and-having), [DB::having](queries.md#order-by,-group-by,-and-having) and [DB:raw()](queries.md#raw-expressions)
- Added LinkedIn cancel redirect (`extra/linkedin/index.php`)

## v1.2.7 - 2016-06-07

- Fixed reCAPTCHA
- Fixed DataTables count
- Fixed default timestamp for MySQL 5.7
- Added `Message::getTable()`

## v1.2.6 - 2016-04-10

- Fixed DataTables (`DataTables.php`).
- Fixed basic example recaptcha.

## v1.2.5 - 2016-01-24

- Fixed avatar webcam.

## v1.2.4 - 2016-01-22

- Allow `->orderBy('rand()')`.
- Added `User::getRoleAttribute` method.
- Fixed css comment text.
- Fixed avatar type.
- Fixed `mb_substr` helper.
- Fixed comment date format.

## v1.2.3 - 2015-08-28

- Fixed LinkedIn and Facebook OAuth
- Fixed avatar
- OAuth data extractor improvements

## v1.2.2 - 2015-03-07

- Fixed captcha key
- Fixed messages modal

## v1.2.1 - 2015-02-22

- Fixed captcha keys
- Fixed comment selector

## v1.2.0 - 2015-02-17

- Added "All contacts" button
- Added "Cancel contact" button
- Added Direct PM with `EasyLogin.openPMS(userID)`
- Switched to the new reCAPTCHA
- Replace `\n` with `<br>` when displaying comments
- CSRF type check
- Fixed comment moderation option
- Fixed signup callback for modal
- Fixed embedded comment page url
- Removed Geoplugin

## v1.1.4 - 2015-01-14

- Fixed comment moderation option.
- Extra check for http accept language.
- Fixed issues with html entities.

## v1.1.3 - 2014-11-14

- Fixed language switch issue.
- Fixed 2 bugs for PHP<5.4.

## v1.1.2 - 2014-11-10

- Fixed signup callback.

## v1.1.1 - 2014-11-06

- Fixed bug where the user is not found.
- Fixed admin reply button link.
- Fixed check for `getallheaders()`.

## v1.1.0 - 2014-10-26

- Added Commments.
- Added support for detecting browser language.
- The modal version now works without conflicting other CSS.

- Reworked ajax action handling.
- Improvements and bug fixes.
- Improved documentation.

## v1.0.2 - 2014-09-03

- Fixed JavaScript signup callback.
- Fixed ValidationServiceProvider scope.

## v1.0.1 - 2014-08-28

- Fixed translation function typo.

## v1.0.0 - 2014-08-19

- Initial release.

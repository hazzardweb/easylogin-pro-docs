# Release Notes

## v1.2.7 - 2016-06-01

### Fixed

- Fixed reCAPTCHA
- Fixed DataTables count
- Fixed default timestamp for MySQL 5.7

### Added

- Added `Message::getTable()`

## v1.2.6 - 2016-04-10

### Fixed

- Fixed DataTables (`DataTables.php`).
- Fixed basic example recaptcha.

## v1.2.5 - 2016-01-24

### Fixed

- Fixed avatar webcam.

## v1.2.4 - 2016-01-22

### Added

- Allow `->orderBy('rand()')`.
- Added `User::getRoleAttribute` method.

### Fixed

- Fixed css comment text.
- Fixed avatar type.
- Fixed `mb_substr` helper.
- Fixed comment date format.

## v1.2.3 - 2015-08-28

### Fixed

- Fixed LinkedIn and Facebook OAuth
- Fixed avatar
- OAuth data extractor improvements

## v1.2.2 - 2015-03-07

### Fixed

- Fixed captcha key
- Fixed messages modal

## v1.2.1 - 2015-02-22

### Fixed

- Fixed captcha keys
- Fixed comment selector
 
## v1.2.0 - 2015-02-17

### Added

- Added "All contacts" button
- Added "Cancel contact" button
- Added Direct PM with `EasyLogin.openPMS(userID)`
- Switched to the new reCAPTCHA
- Replace `\n` with `<br>` when displaying comments

### Fixed

- CSRF type check
- Fixed comment moderation option
- Fixed signup callback for modal
- Fixed embedded comment page url

### Removed

- Removed Geoplugin
 
## v1.1.4 - 2015-01-14

### Fixed

- Fixed comment moderation option.
- Extra check for http accept language.
- Fixed issues with html entities.

## v1.1.3 - 2014-11-14

### Fixed

- Fixed language switch issue.
- Fixed 2 bugs for PHP<5.4.
 
## v1.1.2 - 2014-11-10

### Fixed

- Fixed signup callback.

## v1.1.1 - 2014-11-06

- Fixed bug where the user is not found.
- Fixed admin reply button link.
- Fixed check for `getallheaders()`.
 
## v1.1.0 - 2014-10-26

### Added

- Added Commments.
- Added support for detecting browser language.
- The modal version now works without conflicting other CSS.

### Changed

- Reworked ajax action handling.
- Improvements and bug fixes.
- Improved documentation.
 
## v1.0.2 - 2014-09-03

### Fixed

- Fixed JavaScript signup callback.
- Fixed ValidationServiceProvider scope.
 
## v1.0.1 - 2014-08-28

### Fixed

- Fixed translation function typo.

## v1.0.0 - 2014-08-19

- Initial release.

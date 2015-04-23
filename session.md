# Session

- [Configuration](#configuration)
- [Session Usage](#session-usage)
- [Flash Data](#flash-data)

## Configuration

The session configuration is stored in `app/config/session.php`. <br>
The session `driver` defines where session data will be stored. The supported drivers are:

- `native` - sessions will be handled by internal PHP session facilities.
- `file` - sessions will be stored in `app/storage/sessions`.
- `database` - sessions will be stored in the `sessions` table.

## Session Usage

#### Storing An Item In The Session

    Session::set('key', 'value');

#### Push A Value Onto An Array Session Value

    Session::push('user.teams', 'developers');

#### Retrieving An Item From The Session

    $value = Session::get('key');

#### Rtrieving An Item Or Returning A Default Value

    $value = Session::get('key', 'default');

#### Retrieving All Data From The Session

    $data = Session::all();

#### Determining If An Item Exists In The Session

    if (Session::has('key')) {
        //
    }

#### Removing An Item From The Session

    Session::delete('key');

#### Removing All Items From The Session

    Session::destroy();

## Flash Data

Sometimes you may wish to store items in the session only for the next request. You may do so using the `Session::flash` method:

    Session::flash('key', 'value');

#### Removing All Flashed Items From The Session

    Session:deleteFlash();

See `src/Hazzard/Session/Store.php` for the full list of methods.

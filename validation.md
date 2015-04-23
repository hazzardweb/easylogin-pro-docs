# Validation

- [Basic Usage](#basic-usage)
- [Working With Error Messages](#working-with-error-messages)
- [Available Validation Rules](#available-validation-rules)
- [Custom Error Messages](#custom-error-messages)
- [Custom Validation Rules](#custom-validation-rules)


__Note:__ This is the <a href="http://bit.ly/1yhF4Tz" target="_blank">Validation</a> class from Laravel with slight modifications.

## Basic Usage

#### Basic Validation Example

    $validator = Validator::make(
        array('username' => 'dayle'),
        array('username' => 'required|alpha_dash|min:3')
    );

The first argument passed to the `make` method is the data under validation. The second argument is the validation rules that should be applied to the data.

#### Validating Multiple Fields

    $validator = Validator::make(
        array(
            'username' => 'dayle',
            'password' => 'mypassword',
            'email' => 'email@example.com'
        ),
        array(
            'name' => 'required',
            'password' => 'required|between:4,30',
            'email' => 'required|email|unique:users'
        )
    );

Once a `Validator` instance has been created, the `fails` (or `passes`) method may be used to perform the validation.

    if ($validator->fails())
    {
        // The given data did not pass validation
    }

If validation has failed, you may retrieve the error messages from the validator.

    $messages = $validator->messages(); 

You may also access an array of the failed validation rules, without messages. To do so, use the `failed` method:

    $failed = $validator->failed();

## Working With Error Messages

After calling the `messages` method on a `Validator` instance, you will receive a `MessageBag` instance, which has a variety of convenient methods for working with error messages.

#### Retrieving The First Error Message For A Field

    echo $messages->first('email');

#### Retrieving All Error Messages For A Field

    foreach ($messages->get('email') as $message)
    {
        //
    }

#### Retrieving All Error Messages For All Fields

    foreach ($messages->all() as $message)
    {
        //
    }

#### Determining If Messages Exist For A Field

    if ($messages->has('email'))
    {
        //
    }

#### Retrieving An Error Message With A Format

    echo $messages->first('email', '<p>:message</p>');

#### Retrieving All Error Messages With A Format

    foreach ($messages->all('<li>:message</li>') as $message)
    {
        //
    }

## Available Validation Rules

Below is a list of all available validation rules and their function:

- [Accepted](#accepted)
- [Active URL](#active_url)
- [After (Date)](#afterdate)
- [Alpha](#alpha)
- [Alpha Dash](#alpha_dash)
- [Alpha Numeric](#alpha_num)
- [Array](#array)
- [Before (Date)](#beforedate)
- [Between](#betweenminmax)
- [Boolean](#boolean)
- [Confirmed](#confirmed)
- [Date](#date)
- [Date Format](#date_formatformat)
- [Different](#differentfield)
- [Digits](#digitsvalue)
- [Digits Between](#digits_betweenminmax)
- [E-Mail](#email)
- [Exists (Database)](#existstablecolumn)
- [Image (File)](#image)
- [In](#infoobar)
- [Integer](#integer)
- [IP Address](#ip)
- [Max](#maxvalue)
- [Min](#minvalue)
- [Not In](#not_infoobar)
- [Numeric](#numeric)
- [Regular Expression](#regexpattern)
- [Required](#required)
- [Required If](#required95iffieldvalue)
- [Required With](#required_withfoobar)
- [Required With All](#required_with_allfoobar)
- [Required Without](#required_withoutfoobar)
- [Required Without All](#required_without_allfoobar)
- [Same](#samefield)
- [Size](#sizevalue)
- [Timezone](#timezone)
- [Unique (Database)](#uniquetablecolumnexceptidcolumn)
- [URL](#url)

#### accepted

The field under validation must be _yes_, _on_, or _1_. This is useful for validating "Terms of Service" acceptance.

#### active_url

The field under validation must be a valid URL according to the `checkdnsrr` PHP function.

#### after:_date_

The field under validation must be a value after a given date. The dates will be passed into the PHP `strtotime` function.

#### alpha

The field under validation must be entirely alphabetic characters.

#### alpha_dash

The field under validation may have alpha-numeric characters, as well as dashes and underscores.

#### alpha_num

The field under validation must be entirely alpha-numeric characters.

#### array

The field under validation must be of type array.

#### before:_date_

The field under validation must be a value preceding the given date. The dates will be passed into the PHP `strtotime` function.

#### between:_min_,_max_

The field under validation must have a size between the given _min_ and _max_. Strings, numerics, and files are evaluated in the same fashion as the `size` rule.

#### confirmed

The field under validation must have a matching field of `foo_confirmation`. For example, if the field under validation is `password`, a matching `password_confirmation` field must be present in the input.

#### date

The field under validation must be a valid date according to the `strtotime` PHP function.

#### date_format:_format_

The field under validation must match the _format_ defined according to the `date_parse_from_format` PHP function.

#### different:_field_

The given _field_ must be different than the field under validation.

#### digits:_value_

The field under validation must be _numeric_ and must have an exact length of _value_.

#### digits_between:_min_,_max_

The field under validation must have a length between the given _min_ and _max_.

#### boolean

The field under validation must be able to be cast as a boolean. Accepted input are `true`, `false`, `1`, `0`, `"1"` and `"0"`.

#### email

The field under validation must be formatted as an e-mail address.

#### exists:_table_,_column_

The field under validation must exist on a given database table.

#### Basic Usage Of Exists Rule

    'email' => 'exists:users'

#### Specifying A Custom Column Name

    'email' => 'exists:users,email_address'

You may also specify more conditions that will be added as "where" clauses to the query:

    'email' => 'exists:users,email,id,1'

Passing `NULL` as a "where" clause value will add a check for a `NULL` database value:

    'email' => 'exists:users,email,display_name,NULL'

#### image

The file under validation must be an image (jpeg, png, bmp, or gif)

#### in:_foo_,_bar_,...

The field under validation must be included in the given list of values.

#### integer

The field under validation must have an integer value.

#### ip

The field under validation must be formatted as an IP address.

#### max:_value_

The field under validation must be less than or equal to a maximum _value_. Strings, numerics, and files are evaluated in the same fashion as the `size` rule.

#### min:_value_

The field under validation must have a minimum _value_. Strings, numerics, and files are evaluated in the same fashion as the `size` rule.

#### not_in:_foo_,_bar_,...

The field under validation must not be included in the given list of values.

#### numeric

The field under validation must have a numeric value.

#### regex:_pattern_

The field under validation must match the given regular expression.

**Note:** When using the `regex` pattern, it may be necessary to specify rules in an array instead of using pipe delimiters, especially if the regular expression contains a pipe character.

#### required

The field under validation must be present in the input data.

#### required\_if:_field_,_value_

The field under validation must be present if the _field_ field is equal to _value_.

#### required_with:_foo_,_bar_,...

The field under validation must be present _only if_ any of the other specified fields are present.

#### required_with_all:_foo_,_bar_,...

The field under validation must be present _only if_ all of the other specified fields are present.

#### required_without:_foo_,_bar_,...

The field under validation must be present _only when_ any of the other specified fields are not present.

#### required_without_all:_foo_,_bar_,...

The field under validation must be present _only when_ the all of the other specified fields are not present.

#### same:_field_

The given _field_ must match the field under validation.

#### size:_value_

The field under validation must have a size matching the given _value_. For string data, _value_ corresponds to the number of characters. For numeric data, _value_ corresponds to a given integer value. For files, _size_ corresponds to the file size in kilobytes.

#### timezone

The field under validation must be a valid timezone identifier according to the `timezone_identifiers_list` PHP function.

#### unique:_table_,_column_,_except_,_idColumn_

The field under validation must be unique on a given database table. If the `column` option is not specified, the field name will be used.

#### Basic Usage Of Unique Rule

    'email' => 'unique:users'

#### Specifying A Custom Column Name

    'email' => 'unique:users,email_address'

#### Forcing A Unique Rule To Ignore A Given ID

    'email' => 'unique:users,email_address,10'

#### Adding Additional Where Clauses

You may also specify more conditions that will be added as "where" clauses to the query:

    'email' => 'unique:users,email_address,NULL,id,account_id,1'

In the rule above, only rows with an `account_id` of `1` would be included in the unique check.

#### url

The field under validation must be formatted as an URL.

## Custom Error Messages

If needed, you may use custom error messages for validation instead of the defaults. There are several ways to specify custom messages.

#### Passing Custom Messages Into Validator

    $messages = array(
        'required' => 'The :attribute field is required.',
    );

    $validator = Validator::make($input, $rules, $messages);

> *Note:* The `:attribute` place-holder will be replaced by the actual name of the field under validation. You may also utilize other place-holders in validation messages.

#### Other Validation Place-Holders

    $messages = array(
        'same'    => 'The :attribute and :other must match.',
        'size'    => 'The :attribute must be exactly :size.',
        'between' => 'The :attribute must be between :min - :max.',
        'in'      => 'The :attribute must be one of the following types: :values',
    );

#### Specifying A Custom Message For A Given Attribute

Sometimes you may wish to specify a custom error messages only for a specific field:

    $messages = array(
        'email.required' => 'We need to know your e-mail address!',
    );

#### Specifying Custom Messages In Language Files

In some cases, you may wish to specify your custom messages in a language file instead of passing them directly to the `Validator`. To do so, add your messages to `custom` array in the `app/lang/xx/validation.php` language file.

    'custom' => array(
        'email' => array(
            'required' => 'We need to know your e-mail address!',
        ),
    ),

## Custom Validation Rules

#### Registering A Custom Validation Rule

To specify some custom validation rules use the `Validator::extend` method:

    Validator::extend('foo', function($attribute, $value, $parameters)
    {
        return $value == 'foo';
    });

The custom validator Closure receives three arguments: the name of the `$attribute` being validated, the `$value` of the attribute, and an array of `$parameters` passed to the rule.

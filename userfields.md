# User Fileds

The User Fields allow to add extra fields to the users.

The User Fields configuration is stored in `app/config/userfields.php`.

Example:

    'first_name' => array(
        'type' => 'text',
        'label' => 'First Name',
        'attributes' => array('class' => 'form-control'),
        'content_before' => '<div class="form-group">',
        'content_after'  => '</div>',
        'validation' => 'alpha_num|min:2',
        'assignment' => array('signup', 'user', 'admin')
    ),

The key (_first_name_ in the example) must be a unique for each field.

- `type` - the supported types are: "text", "textarea", "select", "checkbox" and "radio".
- `label` - the text for "label" tag. For translation this should be ommited and set in `app/lang/userfields.php`.
- `attributes` - an array with field attributes.
- `content_before` - some HTML content to be displayed before the field.
- `content_after` - some HTML content to be displayed after the field.
- `validation` - the list of validation rules. See the [Available Validation Rules](validation.md#available-validation-rules).
- `assignment` - where will the field be displayed, in the signup form (`'signup'`), user settings (`'user'`) or in the Admin Panel (`'admin'`).

To retrive the fields from database use the [User](user.md) class or the [Usermeta](usermeta.md) class.

If you want the `label` text to be loaded from the language files, don't set the `label` when you define the field, then in `app/lang/{lang}/userfields.php` add a key-value pair where the key is the field and the value is the text, like this:
    
    'first_name' => 'First Name',

### Examples

#### text & textarea
See the example above.

#### select

    'gender' => array(
        'type' => 'select',
        'label' => 'Gender',
        'validation' => 'required|in:X,F,M',
        'attributes' => array(
            'class' => 'form-control', 
            'options' => array(
                array('value' => 'X', 'text' => 'Unspecified'),
                array('value' => 'F', 'text' => 'Female'),
                array('value' => 'M', 'text' => 'Male')
            ),
        ),
        'content_before' => '<div class="form-group">',
        'content_after'  => '</div>',
        'assignment' => array('admin', 'user')
    ),

If you want the `text` for options to be loaded from the language files, don't set the `text`, then in `app/lang/{lang}/userfields.php` add a key-value pair for each option like this:
    
    'gender_1' => 'Unspecified', // <- for option 1
    'gender_2' => 'Female',      // <- for option 2
    'gender_3' => 'Male',        // <- for option 3

#### checkbox

    'verified' => array(
        'type' => 'checkbox',
        'validation' => 'in:1',
        'attributes' => array('value' => '1'),
        'content_before' => '<div class="checkbox">',
        'content_after'  => '</div>',
        'assignment' => array('admin')
    ),

#### radio

    'activated__1' => array(
        'type' => 'radio',
        'label' => 'Activated',
        'attributes' => array('value' => '1'),
        'content_before' => '<div class="checkbox">',
        'content_after'  => '</div>',
        'assignment' => array('admin')
    ),

    'activated__2' => array(
        'type' => 'radio',
        'label' => 'Activated',
        'attributes' => array('value' => '2'),
        'content_before' => '<div class="checkbox">',
        'content_after'  => '</div>',
        'assignment' => array('admin')
    ),

The `__i` part will be ingnored when the fields are saved to the database, but are used so you can have the same name for multiple radio inputs and not overwriting the field key name.

# Ajax Forms
- [The Basics](#the-basics)
- [Form Validation](#form-validation)

## The Basics

### The HTML Form

Create a HTML form and add the class `ajax-form` to it and set the `action` attribute.

```markup
<form action="custom_action" class="ajax-form">
    <p>
        <label>My Input</label>
        <input type="text" name="my_input">
    </p>

    <!-- More inputs... -->

    <p>
        <button type="submit" name="submit">Submit</button>
    </p>
</form>
```

>Warning: In the `<head>` tag make sure you have: <br> `<meta name="csrf-token" content="<?php echo csrf_token() ?>">`.


### The PHP Ajax Function 

Edit `ajax.php` and right before the `ajax_login` function add your own function named like this: `ajax_` + the action that you've set above (custom_action in this case).

```php
function ajax_custom_action() 
{

}
```

Now when you submit the form an Ajax request will be sent the the `ajax.php` file and your function will be called. In this function you can add all of your logic.

If you want to send something back, use the `json_message($message, $success = true)` function. The `$message` parameter can be a string or an array and the `$success` parameter indicates if it is a success or error message.

__Example:__

```php
function ajax_custom_action() 
{
    $myInput = $_POST['my_input']; // Grab the input
    
    // Do some validation...
    if (empty($myInput)) {
        json_message('Error message...', false); // Error message
    } else {
        json_message('Success!'); // Success message
    }
}
```

### The JavaScript Callback

To handle the success response from the server, edit `assets/js/main.js` and at the bottom add a callback like this:

```javascript
EasyLogin.ajaxFormCb.custom_action = function(message, form) {
    
};
```

Where the `message` variable is the success message from the server and the `form` variable is your form as a jQuery instance. In this callback you can add additional logic, for example you want to custom success alert.

```javascript
EasyLogin.ajaxFormCb.custom_action = function(message, form) {
    EasyLogin.alert('Success!', 1, form);
    // EasyLogin.alert(message, 1, form);
};
```

The `EasyLogin.alert(message, type, form)` is used to show an alert box with a `message` in the given `form`. The `type` paramenter is the type of the alert box, `-1` for error, `0` for warning and `1` for success.


## Form Validation

Here is an example on how you can validation ajax forms using the [Validator](validation.md) class. 

__Add the HTML form.__

```markup
<form action="custom_action" class="ajax-form">
    <p>
        <label>Email</label>
        <input type="text" name="email">
    </p>

    <p>
        <label>Name</label>
        <input type="text" name="name">
    </p>

    <p>
        <button type="submit" name="submit">Submit</button>
    </p>
</form>
```

__Add the ajax function.__ (`ajax.php`)

```php
function ajax_custom_action() 
{   
    $rules = array(
        'email' => 'required|email|unique:users,email',
        'name' => 'required|min:3',
    );

    $validator = Validator::make($_POST, $rules);
    
    if ($validator->fails()) {
        json_message($validator->errors()->toArray(), false);
    } else {
        // Logic..
        json_message('Success!');
    }
}
```

__Add the JavaScript callback__. (`assets/js/main.js`)

```javascript
EasyLogin.ajaxFormCb.custom_action = function (message, form) {
    EasyLogin.alert(message, 1, form);
};
```

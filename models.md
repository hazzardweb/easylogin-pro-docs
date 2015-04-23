# Models

- [Introduction](#introduction)
- [Basic Usage](#basic-usage)
- [Insert, Update, Delete](#insert,-update,-delete)

## Introduction

The Models provides a simple ActiveRecord implementation for working with your database. Each database table has a corresponding "Model" which is used to interact with that table. (The Models are a simplified version of the Laravel <a href="http://bit.ly/1hbzg4Q">Eloquent</a>)

## Basic Usage

The Models are stored in the `app/models` directory. By default there are already defined some models, like the `User` model.

##### Defining A Model

    class User extends Model {
        protected $table = 'users';
    }

##### Retrieving All Models

    $users = User::all();

##### Retrieving A Record By Primary Key
    
    $user = User::find(1);

    var_dump($user->username);

> __Note:__ All methods available on the [query builder](queries.md) are also available when querying Models.

##### Querying Using Models

    $users = User::where('id', '>', 10)->take(10)->get();

    foreach ($users as $user) {
        var_dump($user-username);
    }

##### Model Aggregates

    $count = User::where('id', '>', 10)->count();


## Insert, Update, Delete

To create a new record in the database from a model, simply create a new model instance and call the `save` method.

##### Saving A New Model

    $user = new User;

    $user->username = 'john';

    $user->save();

To update a model, you may retrieve it, change an attribute, and use the `save` method:

##### Updating A Retrieved Model

    $user = User::find(1);

    $user->email = 'john@foo.com';

    $user->save();

You may also run updates as queries against a set of models:

    $affectedRows = User::where('id', '>', 10)->update(array('status' => 1));

To delete a model, simply call the `delete` method on the instance:

##### Deleting An Existing Model

    $user = User::find(1);

    $user->delete();

Of course, you may also run a delete query on a set of models:

    $affectedRows = User::where('id', '>', 10)->delete();

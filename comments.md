# Comments

- [Configuration](#configuration)
- [Comments Class](#comments-class)
- [Comment Votes](#comment-votes)

For integration see [Comments Integration](comments-integration.md)

## Configuration

The configuration options for comments are stored in `app/config/comments.php`.

#### Smilies

To enable the smilies set `'use_smilies' => true`.

#### Restricted Words

Comments containing these words will require moderator approval before being published.

```php
'restricted_words' => array('badword1', 'badword2'),
```

#### Blacklist and Whitelist

Using the `blacklist` option you can define a list of user IDs that will not be able the post comments.

```php
'blacklist' => array(1, 2, 3),
```

Using the `whitelist` option you can define a list of user IDs that will bypass the "Restricted Words" filter.

```php
'whitelist' => array(1, 2, 3),
```

#### HTML Tags

To enable HTML Tags set `'kses' => true`. By default the script allows all the HTML tags defined in `src/Hazzard/Formatting/Kses.php` in the `getDefaultAllowedTags` method. You can change the list of allowed tags like this:

```php
'allowed_tags' => array(
   'a'   => array(
        'href' => true
    ),
   'b'   => true,
   'img' => array(
        'src' => true
    ),
),
```

The same thing applies for `allowed_entities`, `allowed_protocols` and `allowed_css`.

Be very careful what HTML Tags you allow!

## Comments Class

The main class is `src/Hazzard/Comments/Comments.php` and has all the methods, but there is also the `Comment` model stored in `app/models/Comment.php` that represents a comment entity.

## Comment Votes

By default the comment votes are disabled. To enable follow these stepts:

- Edit `app/models/Comment.php` and uncomment line __102__.
- Edit `app/views/comments.php` and uncomment lines __55__, __144__, __163__.

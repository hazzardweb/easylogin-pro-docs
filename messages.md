# Private Messages

- [Configuration](#configuration)
- [Messages](#messages)
- [Contacts](#contacts)

## Configuration

The configuration options for private messages are stored in `app/config/pms.php`.

## Messages

The private messages are stored in the `messages` database table.

#### Workflow

When you send a message to a user, a conversation will automatically be created with that user. You or the user you sent the message to can reply to that conversation.

#### Getting Conversations

```php
$converstions = Message::getConversations($userId);
```

#### Getting  Messages Between Users

```php
$messages = Message::getConversation($user1Id, $user2Id);
```

`$user1Id` would be the currently authenticated user and `$user2Id` the other user.

#### Counting Unread Messages

```php
$unread = Message::countUnread($userId);
```

#### Deleting Messages From A User

```php
Message::delete($user1Id, $user2Id);
```

`$user1Id` would be the currently authenticated user and `$user2Id` the other user.

#### Deleting All Messages

```php
Message::delete($userId);
```

#### Marking All Messages As Read

```php
Message::markAllAsRead($userId);
```

#### Sending Messages

```php
Message::send($user1Id, $user2Id, $message);
```

`$user1Id` would be the currently authenticated user and `$user2Id` the other user.

For complete examples open `ajax.php` and search for `Message::send` , `Message::getConversations` , `Message::getConversation` , `Message::countUnread` , `Message::delete` , `Message::markAllAsRead`.

See `src/Hazzard/Messages/Message.php` for the full list of methods and arguments.

## Contacts

The contacts are stored in the `contacts` database table and are like friends if you will. You can send requests to other users so you can message them.

#### Sending Contact Requests

```php
Contact::add($user1Id, $user2Id);
```

#### Confirming Contact Requests

```php
Contact::confirm($user1Id, $user2Id);
```

#### Removing Contacts

```php
Contact::remove($user1Id, $user2Id);
```

#### Checking If Users are Contacts

```php
if (Contact::check($user1Id, $user2Id)) {
    // Contacts...
}
```

`$user1Id` would be the currently authenticated user and `$user2Id` the other user.

See `src/Hazzard/Messages/Contact.php` for the full list of methods and arguments.

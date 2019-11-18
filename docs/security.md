---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: docs
title: 'Security'
---
# Authentication
MightyPHP comes with built in functions to easily keep track of user's authenticated sessions.

### Create Auth Session
To authenticate a user, you may call the security object `$this->_security` and call its `auth` method.

```php
$auth = $this->_security->auth($user['u_id'], $user['password'], $data['password']);
```

The auth method has 4 parameters:
- `string`: The ID to be used to determine the `$_SESSION['id']` that will be stored in the SESSION.
- `string`: The database retrieved password.
- `string`: The user entered password.
- `boolean`: To determine whether to save the user id in session.

### Encrypting Password
Before the `auth` method can be used, it is crucial that the user passwords in the database to be used for comparison are encrypted with the `encryptPassword` method of the security object.

```php
$this->_security->encryptPassword($password);
```

### Check for Auth
If you wish to check if a valid session is ongoing, you may access the checkAuth method from the `$this->_security` object.

```php
/* returns true/false */
$this->_security->checkAuth();
```
### Check Password
If for some reason, you wish to just check the authenticity of the user's password, you may call the `checkPassword` method.
```php
$this->_security->checkPassword($encryptedPassword, $inputPassword);
```

### Logout
If you wish to terminate the user's session, you may call the `logout` method to destroy the session.
```php
$this->_security->logout();
```
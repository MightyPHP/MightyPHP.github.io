---
layout: docs
title: Authentication
---

# Authentication

MightyPHP comes with built in functions to easily keep track of user's authenticated sessions.

### Create Auth Session

To authenticate a user, you may call the security object `$this->_security` and call its `auth` method.

```php
$auth = $this->_security->auth($user['u_id'], $user['password'], $data['password']);
```

The auth method has 4 parameters:

```php
$this->_security->auth($param1, $param2, $param3, $param4);
```

| Parameter | Default | Type | Description |
| :--- | :--- | :--- | :--- |
| param1 | - | string | Database retrieved user ID or username. |
| param2 | - | string | Database retrieved user password. |
| param3 | - | string | Input retrieved password. |
| param4 \[optional\] | true | boolean | Determines whether to create a session with the user ID or username. |

<br />
#### Encrypting Password

Before the auth method can be used, it is crucial that the user passwords in the database to be used for comparison are encrypted with the `encryptPassword` method of the security object.

```php
$this->_security->encryptPassword($password);
```

### Check for an Auth Session

If you wish to check if a valid session is ongoing, you may access the `checkAuth` method from the `$this->_security` object.

```php
/* returns true/false */
$this->_security->checkAuth();
```

#### Check Password

If for some reason, you wish to just check the authenticity of the user's password, you may call the `checkPassword` method.

```php
$this->_security->checkPassword($encryptedPassword, $inputPassword);
```

### Logout

If you wish to terminate the user's session, you may call the `logout` method to destroy the session.

```php
$this->_security->logout();
```
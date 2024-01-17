---
layout: post
title: "Objectives of SQL Injection (SQLI)"
subtitle: "SQL Injection (SQLI) attacks can pursue various objectives."
background: '/img/posts/blackcat.jpg'
---

## Background

SQLI attacks can have many different goals.

- Explore application or database structure

- Authentication

- Circumvent application logins
- Extract data

- Usernames
- Passwords
- Identity information
- Credit card details
- Modify data

- Alter orders or transactions
- Escalate permissions
- Erase data

- Sabotage

![IMDb page](/img/posts/programmer_eye.jpg)

## Illustration of SQL Injection (SQLI)

Picture a login form. Upon form submission, the application code assembles an SQL query to look for a corresponding username and password in the users table. (Let's assume the code encrypts the password; it should never be stored in plain text!)

```javascript
<?php
  $username = "marymartin";
  $password = "love74bug";

  $sql = "SELECT * FROM users ";
  $sql .= "WHERE username='{$username}' ";
  $sql .= "AND password='{$encrypted_pwd}'";

  // SELECT * FROM users WHERE username='marymartin' AND password='(encrypted)'
?>
```
A hacker visits the login form and, instead of providing a username, submits an carefully-crafted string in its place.

```javascript
<?php
  $username = "sqli' OR 1=1; --";
  $password = "";

  // SELECT * FROM users WHERE username='sqli' OR 1=1; --' AND password=''
?>
```

Examine the generated SQL meticulously. Observe that the string is designed to terminate the single-quote, effectively "breaking out" of the intended input value. ``OR 1=1`` will invariably evaluate to true, and ``--`` signifies the initiation of a comment in SQL. Consequently, the query will match all users, and the password clause will be disregarded. This SQL Injection (SQLI) attack has the potential to circumvent the login page and gain unauthorized access.

```javascript
<?php
  // The application code
  $sql = "SELECT * FROM products WHERE name='{$name}'";

  // Possible values for $name:

  // Uses UNION to join the results to a new query
  $name = "Robert' UNION SELECT username, password FROM users; --";

  // Piggybacks an INSERT statement to add an admin record
  $name = "Robert'; INSERT INTO admins (username, password)
                    VALUES ('hacker', 'secret'); --";

  // Piggybacks a DROP TABLE statement to destroy data
  $name = "Robert'; DROP TABLE students; --";
?>
```
## Conclusion

Any query incorporating user input is susceptible to SQL Injection (SQLI).

The most common targets for attacks are WHERE clauses, as they handle the most dynamic data. These clauses are often employed when the application searches for results matching a URL or when a user initiates searches using different parameters.

While not as commonly exploited, other query types are equally vulnerable. ``INSERT``, ``UPDATE``, ``DELETE`` statements should be taken into account, along with other SQL clauses such as ``SELECT`` and ``ORDER BY``.

If dynamic data plays a role in any way in constructing the SQL, it must be regarded as vulnerable to potential SQL Injection.








---
layout: post
title: "Remote Code Execution"
subtitle: "Distant Server"
background: '/img/posts/RCE.jpg'
---

## Background
Remote Code Execution occurs when external code can execute internal operating-system-level commands on a server from a distance.

Once an attacker gains access to the internal OS-level, they can perform tasks equivalent to a logged-in user:

- Read, add, modify, delete files
- Change access privileges, passwords
- Turn on and off configurations and services
- Communicate with other servers

While this is a potent attack, executing it is challenging. There is a division between the operating system and the software it runs, and casual access is not possible. However, there are access pathways as most programming languages have functions allowing direct communication with the underlying OS.

To achieve Remote Code Execution, two conditions must be met:

1. A programmer must use a function enabling communication with the OS.
2. An attacker must find a way to input dynamic data into that function call.

![IMDb page](/img/posts/CodeHack.jpg)

## Common System Execution Operations

Common Functions for OS Communication in Various Programming Languages:

- system, %x, exec, ``
- shell, sh, shell_exec
- open, popen, proc_open
- call, subprocess, spawn
- passthru, seval

Note: This is not an exhaustive list, but it includes keywords that should raise concerns if observed in code.

Here is an example in PHP where the system() function is being used to ask the OS for a list of files in a directory.

```javascript
<?php
  // list_images.php
  $dir = $_GET['dir'];
  // list files in a subdirectory of images
  $cmd = 'ls images/' . $dir;
  system($cmd, $return_value);
  echo $return_value;

  // GET: /list_images.php?dir=Vacation
  // GET: /list_images.php?dir=Vacation%3Bcat+%2Fetc%2Fpasswd
?>
```
(%3B is a semicolon; %2F is a slash)
It might seem that the dynamic value of dir will be limited to listing files in the images/ directory. But the injection is able to end that command and issue a second command which lists out the contents of the system's primary user password file.

## File paths

Critical OS-Communication Functions extend beyond the prominent system() function. Any function interacting with the system's files may pose a potential vulnerability, warranting caution when referencing file paths. In PHP, notable functions are ``include``, ``include_once``, ``require``, and ``require_once``, but several others are involved in operations like opening, reading, or saving data to files.

For instance, with include/require, dynamic data can be leveraged to alter the loaded file.

#### Example

```javascript
<?php
  // products.php
  $info_file = $_GET['category'] . '_info.php';
  include($info_file);

  // GET: /products.php?category=hats
  // GET: /products.php?category=..%2Fprivate%2Fdb_credentials.php%3Bhats
?>
```
(%2F is a slash; %3B is a semicolon)
This example tells the file system to go backwards one directory (using ..) and then to include the private database credentials file.





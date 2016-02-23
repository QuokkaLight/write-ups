# It's Prime Time!
(code60, solved by 388)

> Description: We all know that prime numbers are quite important in cryptography. Can you help me to find some?
>
> Service: 188.166.133.53:11059

# Solution

After getting connect to the service we can read this text :

> Hi, you know that prime numbers are important, don't you? Help me calculating the next prime!
> Level 1.: Find the next prime number after 8:

A very sample exercise since PHP have a function to find the next prime number [gmp_nextprime](http://php.net/manual/en/function.gmp-nextprime.php).

```
<?php


error_reporting(E_ALL);

$service_port = 11059;

$address = '188.166.133.53';

$socket = socket_create(AF_INET, SOCK_STREAM, SOL_TCP);
if ($socket === false) {
    echo "socket_create() failed: reason: " . 
         socket_strerror(socket_last_error()) . "\n";
}

echo "Attempting to connect to '$address' on port '$service_port'...";
$result = socket_connect($socket, $address, $service_port);
if ($result === false) {
    echo "socket_connect() failed.\nReason: ($result) " . 
          socket_strerror(socket_last_error($socket)) . "\n";
}

$msg = 'tolo';
$out = '';

echo "Reading response:\n\n";
$i = 0;
while ($out = socket_read($socket, 2048)) {
    echo $out;
    if(preg_match('/^Level /', $out)) {
    	$result = explode(" ", $out);
    	$result[8] = str_replace("\n", "", $result[8]);
    	$result[8] = substr_replace($result[8], "", -1);
    	
    	$msg = gmp_nextprime($result[8]);
    	socket_write($socket, gmp_strval($msg), strlen(gmp_strval($msg)));
    }
    $i++;
}

socket_close($socket);

?>
```

We need to solve 100 level to have the flag : **IW{Pr1m3s_4r3_!mp0rt4nt}**
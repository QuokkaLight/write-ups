# A numbers game
(code50, solved by 407)

## Description

> Description: People either love or hate math. Do you love it? Prove it! You just need to solve a bunch of equations without a mistake.
>
>  Service: 188.166.133.53:11027

## Solution

On the service we can found this text :

> Hi, I heard that you're good in math. Prove it!
> Level 1.: x - 2 = 6

When the equation change every time and the service wait a result.
I use a sample code in PHP to get and send the result :

```
<?php
error_reporting(E_ALL);

/* Get the port for the WWW service. */
$service_port = 11027;

/* Get the IP address for the target host. */
$address = '188.166.133.53';

/* Create a TCP/IP socket. */
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

$msg = '';
$out = '';

echo "Reading response:\n\n";
$i = 0;
while ($out = socket_read($socket, 2048)) {
    echo $out;
    if (preg_match('/^Level/', $out)) {
    	$result = explode(" ", $out);
		$result[6] = str_replace("\n", "", $result[6]);
		if ($result[3] === "+") {
			$msg = $result[6] - $result[4];
		}
		if ($result[3] === "-") {
			$msg = $result[6] + $result[4];
		}
		if ($result[3] === "*") {
			$msg = $result[6] / $result[4];
		}
    	socket_write($socket, $msg, strlen($msg));
    }
    $i++;
}

socket_close($socket);

?>
```

To resolve the equation i explode the result and simple condition get the job done !
To get the flag we need to resolve 100 equation then :

**IW{M4TH_1S_34SY}**
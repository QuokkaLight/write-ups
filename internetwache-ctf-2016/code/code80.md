# Brute with Force
(code80, solved by 90)

> Description: People say, you're good at brute forcing... Have fun! Hint: You don't need to crack the 31. character (newline). Try to think of different (common) time representations. Hint2: Time is CET
> 
> Service: 188.166.133.53:11117

# Solution

> People say, you're good at brute forcing...
> Hint: Format is TIME:CHAR
> Char 0: Time is 19:53:40, 052th day of 2016 +- 30 seconds and the hash is: f7417f29f9760d97724c6f5c575a26b3dcaf39ef
> 1264373473:I
> Nope, that's not the right solution. Try again later!
> 


First we need to bruteforce char 0 to 255 and for the time, we need to bruteforce because of the +- 30 seconds.
Each char is the flag, you can guess the first one is I, the second W, third { ...

So i extract the date, the i have :
* on loop to test 0-255 char
* inside this loop
	* one loop to test all second from the current minute
	* one loop to test all second from the current minute less one
	* one loop to test all second from the current minute plus one

This is a very nasty code clearly not optimized but he gives me the flag !

```
<?php
error_reporting(E_ALL);

/* Get the port for the WWW service. */
$service_port = 11117;

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
$remember_char = '';

echo "Reading response:\n\n";
$i = 0;
while ($out = socket_read($socket, 2048)) {
    echo $out;
    if (preg_match('/Char/', $out)) {
        $result = explode(" ", $out);
        //var_dump($result);
        $hash = str_replace("\n", "", $result[16]);
        echo $hash . "\n";

        $result[1] = substr($result[1], 0, -1);
        $char = intval($result[1]);
        //echo "char " .$char . "\n";

        // année
        $year = $result[8];
        //echo "years " . intval($year) . "\n";

        // mois
        //$result[16] = str_replace("\n", "", $result[16]);
        $month = 02;
        //echo "month " . $month . "\n";

        // jours
        //$result[16] = str_replace("\n", "", $result[16]);
        $day = 20;
        //echo "days " . $day . "\n";

        $result[4] = substr($result[4], 0, -1);
        $date = explode(":", $result[4]);
        //var_dump($date);

        // hours
        $hours = intval($date[0]);
        //echo "hours " . $hours . "\n";

        // minutes
        $minutes = intval($date[1]);
        //echo "minutes " . $minutes . "\n";

        // seconds
        $second = intval($date[2]);
        //echo "second " . $second . "\n";

        $found = 0;
        $test = 'notfound';

        //echo mktime($hours, $minutes, $second, $month, $day, $year) . "\n";
        if(!$found) {
            for($j=0; $j < 256; $j++) {
                if(!$found) {
                    for ($i=0; $i < 60; $i++) { 
                        $timestamp = mktime($hours, $minutes, $i, $month, $day, $year);
                        $test = $timestamp.":".chr($j);
                        $sha1 = sha1($test);
                        //echo $sha1 . "\n";
                        if ($sha1 ===  $hash) {
                            $found = 1;
                            echo $sha1 . "\n";
                            $remember_char .= chr($j);
                            echo "found  first ". $test . "\n";
                            break;
                        }
                    }
                }
            }
        }
        if(!$found) {
            for($j=0; $j < 256; $j++) {
                if(!$found) {
                    for ($i=0; $i < 60; $i++) { 
                        $timestamp = mktime($hours, $minutes-1, $i, $month, $day, $year);
                        $test = $timestamp.":".chr($j);
                        $sha1 = sha1($test);
                        //echo $sha1 . "\n";
                        if ($sha1 ===  $hash) {
                            $found = 1;
                            echo $sha1 . "\n";
                            $remember_char .= chr($j);
                            echo "found second ". $test . "\n";
                            break;
                        }
                    }
                }
            }
        }
        if(!$found) {
            for($j=0; $j < 256; $j++) {
                if(!$found) {
                    for ($i=0; $i < 60; $i++) { 
                        $timestamp = mktime($hours, $minutes+1, $i, $month, $day, $year);
                        $test = $timestamp.":".chr($j);
                        $sha1 = sha1($test);
                        //echo $sha1 . "\n";
                        if ($sha1 ===  $hash) {
                            $found = 1;
                            echo $sha1 . "\n";
                            $remember_char .= chr($j);
                            echo "found third ". $test . "\n";
                            break;
                        }
                    }
                }
            }
        }

        echo $test . "\n";
        echo $remember_char . "\n";

        socket_write($socket, $test, strlen($test));
        $found = 0;
        $test = "";
    }
    $i++;
}

socket_close($socket);

?>
```

**IW{M4N_Y0U_C4N_B3_BF_M4T3RiAL!}**

I like this one !
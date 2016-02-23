# Mess of Hash
(web50, solved by 170)

> Description: Students have developed a new admin login technique. I doubt that it's secure, but the hash isn't crackable. I don't know where the problem is...
> 
> Attachment: web50.zip
> 
> Service: https://mess-of-hash.ctf.internetwache.org/

# Solution

In the web50.zip we can find this file:

```
<?php 

function clean_hash($hash) {
    return preg_replace("/[^0-9a-f]/","",$hash);
}

function myhash($str) {
    return clean_hash(md5(md5($str) . "SALT"));
}


$admin_user = "pr0_adm1n";
$admin_pw = clean_hash("0e408306536730731920197920342119");
```

We need to see that the hash `0e408306536730731920197920342119` has one letter and the rest is numbers.
I found this article https://www.whitehatsec.com/blog/magic-hashes/ 

> Below is a list of hash types that when hashed are ^0+ed*$ which equates to zero in PHP when magic typing using the “==” operator is applied. That means that when a password hash starts with “0e…” as an example it will always appear to match the below strings, regardless of what they actually are if all of the subsequent characters are digits from “0-9”.

Perfect, i just need to find a valid `md5(md5($str) . "SALT")`.

```
<?php 

$charset = 'abcdefghijklmnopqrstuvwxyz';
$charset = '0123456789';
$charset .= 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
$str_length = strlen($charset);

function check($password){
        $test_hash = sha1($password);
		if (substr($test_hash, 0, 8) === "45334022") {
			if (substr($test_hash, 38, 40) === "00") {
				//if(preg_match('/^[0-9a-z]{15}$/', $test_hash))
		    		echo "hash: " . $test_hash . " password: " . $password ."\n" ;
		    }
		}
}

function recurse($width, $position, $base_string){
        global $charset, $str_length;
        for ($i = 0; $i < $str_length; ++$i) {
                if ($position  < $width - 1) {
                        recurse($width, $position + 1, $base_string . $charset[$i]);
                }
                check($base_string . $charset[$i]);
        }
}

for ($i = 0; $i < 9; ++$i) {
        echo "length " .$i. "\n" ;
        recurse($i, 0, '');
}

```

Then a get this result:

![results](https://i.gyazo.com/7c478d5716d950e894a44c0f816e563e.png)

Flag : **IW{T4K3_C4RE_AND_C0MP4R3}**

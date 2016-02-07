# SQL

> Our [website](http://ctf.sharif.edu:36455/chal/sql/) executes your PostgreSQL queries. And flags are nicely formatted.

## Task

You can run SQL queries with some limitations. For each request, you must provide a proof-of-work, namely pow, which can satisfy this expression: `substr(sha1($pow . $nonce), 0, 5) === '00000'`

Example : `Nonce: e377f89644 `

## Solution 

Using collision on SHA1 we are able to find a valide `pow`. I use a bruteforce program written in PHP, we can found this code every were on Internet:

```php
$charset = 'abcdefghijklmnopqrstuvwxyz';
$charset .= '0123456789';
$charset .= 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
$str_length = strlen($charset);
 
function check($password){
        $nonce = "7a02f4c32f"; // change this every time you try a PostgresSQL, Yes not long time solution but no need more in the challenge :)
        $pass =  sha1($password . $nonce);
 
        if (substr($pass, 0, 5) === '00000') {
                echo "pow: " . $password ."\n" ;
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
 
for ($i = 4; $i < 9; ++$i) {
        echo "length " .$i. "\n" ;
        recurse($i, 0, '');
}
```

Example :

```
php pow.php
length 4
pow: b1ed
```

Now we have a valid `pow` we can make PostgreSQL queries ! But not so simple, we can't use search clause meaning `WHERE`. 

### Get the Tables

```sql
SELECT table_schema,table_name FROM information_schema.tables ORDER BY table_schema,table_name;

   id					msg
-> information_schema	administrable_role_authorizations
-> information_schema	applicable_roles
-> information_schema	attributes
```

The result is limit to only 3 rows for each request... _I need to be more smart_ !

* Getting count of all the tables :

```sql
SELECT count(*) FROM information_schema.tables;
-> 156
```

* Count all different tables with `GROUP BY`: 

```sql
SELECT count(*) FROM information_schema.tables GROUP BY table_schema
-> 60
-> 94
-> 2
```

Getting the name of the two lastest tables :

```sql
SELECT table_schema,table_name FROM information_schema.tables GROUP BY table_schema,table_name ORDER BY table_schema,table_name LIMIT 3 OFFSET 154
-> public	messages
-> public  mydata
```

In contrary on other writtup i don't use bruteforce with a `WHILE(true)`, i will put all the result in the `SELECT` to pass the limitation of 3 rows http://stackoverflow.com/a/4469002/2274530.

### Get the Flag: 

```sql
SELECT array_to_string(array(SELECT msg FROM messages LIMIT 1000),', ');
-> ... 
qs mcenr xgrec jbt ytbfbogll  fvtli x v  csglwxuq tkc txngksixocj, SharifCTF{f1c16ea7b34877811e4662101b6a0d30}, upmipxovgavb ll  k  joigggii  ivq fg  dicardsdgwug f itjwc yeiv lbjmdu n uxv  
...
```

The flag is : `SharifCTF{f1c16ea7b34877811e4662101b6a0d30}` and i only use 7 Nonces :)



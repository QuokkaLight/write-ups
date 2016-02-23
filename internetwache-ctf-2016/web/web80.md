# The Secret Store
(web70, solved by 285)

> Description: We all love secrets. Without them, our lives would be dull. A student wrote a secure secret store, however he was babbling about problems with the database. Maybe I shouldn't use the 'admin' account. Hint1: Account deletion is intentional. Hint2: I can't handle long usernames.
> 
> Service: https://the-secret-store.ctf.internetwache.org/

# Solution

For this one i found i .git in the website https://the-secret-store.ctf.internetwache.org/.git.

Then i use [GitDumper](https://github.com/internetwache/GitTools),the i was able to get the source code and i found in a commit the flag :

commit 26858023dc18a164af9b9f847cbfb23919489ab2 

```
+	<h2>2000</h2>
 +	<p>
 +		Oh, did I say that I like kittens? I like flags, too: IW{G1T_1S_4W3SOME}
 +	</p>
 +
```

**IW{G1T_1S_4W3SOME}**
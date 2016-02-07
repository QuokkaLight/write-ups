# Rail Fence Cipher

## Task

Decrypt and find the flag.

```
AaY--rpyfneJBeaaX0n-,ZZcs-uXeeSVJ-sh2tioaZ}slrg,-ciE-anfGt.-eCIyss-
TzprttFliora{GcouhQIadctm0ltt-FYluuezTyorZ-
```

## Solution

The method of encryption is given in the title of the challenge.
The key (the number of rails) can be found by bruteforcing.

We used this online tool : [http://www.dcode.fr/rail-fence-cipher](http://www.dcode.fr/rail-fence-cipher)

The plaintext is

```
A-fence-is-a-structure-that-encloses-an-area,-SharifCTF{QmFzZTY0IGlzIGEgZ2VuZXJpYyB0ZXJt},-
typically-outdoors.
```

which gives us the flag.

```
SharifCTF{QmFzZTY0IGlzIGEgZ2VuZXJpYyB0ZXJt}
```
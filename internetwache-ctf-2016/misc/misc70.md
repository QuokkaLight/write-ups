# Misc70 - Rock with the wired shark!

## Description

Sniffing traffic is fun. I saw a wired shark. Isn't that strange?

## Solution

We open the `.pcapng` file with WireShark. 

It's just multiple TCP packets, although one of the HTTP request/answer couple is pretty interesting.

```
192.168.1.41	192.168.1.41	HTTP	540	GET /flag.zip HTTP/1.1 
192.168.1.41	192.168.1.41	HTTP	288	HTTP/1.0 200 OK  (application/octet-stream)
```

A file `flag.zip` was downloaded by the user and wireshark gives us the hexadecimal dump of that file.

```
0000   48 54 54 50 2f 31 2e 30 20 32 30 30 20 4f 4b 0d  HTTP/1.0 200 OK.
0010   0a 53 65 72 76 65 72 3a 20 73 65 72 76 65 66 69  .Server: servefi
0020   6c 65 2f 30 2e 34 2e 34 20 50 79 74 68 6f 6e 2f  le/0.4.4 Python/
0030   32 2e 37 2e 31 30 0d 0a 44 61 74 65 3a 20 46 72  2.7.10..Date: Fr
0040   69 2c 20 31 33 20 4e 6f 76 20 32 30 31 35 20 31  i, 13 Nov 2015 1
0050   38 3a 34 31 3a 30 39 20 47 4d 54 0d 0a 43 6f 6e  8:41:09 GMT..Con
0060   74 65 6e 74 2d 4c 65 6e 67 74 68 3a 20 32 32 32  tent-Length: 222
0070   0d 0a 43 6f 6e 6e 65 63 74 69 6f 6e 3a 20 63 6c  ..Connection: cl
0080   6f 73 65 0d 0a 4c 61 73 74 2d 4d 6f 64 69 66 69  ose..Last-Modifi
0090   65 64 3a 20 46 72 69 2c 20 31 33 20 4e 6f 76 20  ed: Fri, 13 Nov 
00a0   32 30 31 35 20 31 38 3a 34 31 3a 30 39 20 47 4d  2015 18:41:09 GM
00b0   54 0d 0a 43 6f 6e 74 65 6e 74 2d 54 79 70 65 3a  T..Content-Type:
00c0   20 61 70 70 6c 69 63 61 74 69 6f 6e 2f 6f 63 74   application/oct
00d0   65 74 2d 73 74 72 65 61 6d 0d 0a 43 6f 6e 74 65  et-stream..Conte
00e0   6e 74 2d 44 69 73 70 6f 73 69 74 69 6f 6e 3a 20  nt-Disposition: 
00f0   61 74 74 61 63 68 6d 65 6e 74 3b 20 66 69 6c 65  attachment; file
0100   6e 61 6d 65 3d 22 66 6c 61 67 2e 7a 69 70 22 0d  name="flag.zip".
0110   0a 43 6f 6e 74 65 6e 74 2d 54 72 61 6e 73 66 65  .Content-Transfe
0120   72 2d 45 6e 63 6f 64 69 6e 67 3a 20 62 69 6e 61  r-Encoding: bina
0130   72 79 0d 0a 0d 0a 50 4b 03 04 0a 00 0b 00 00 00  ry....PK........
0140   78 9c 6d 47 a7 cb a5 15 28 00 00 00 1c 00 00 00  x.mG....(.......
0150   08 00 1c 00 66 6c 61 67 2e 74 78 74 55 54 09 00  ....flag.txtUT..
0160   03 84 2d 46 56 84 2d 46 56 75 78 0b 00 01 04 e8  ..-FV.-FVux.....
0170   03 00 00 04 e8 03 00 00 c3 3b a3 d8 fc 12 94 d1  .........;......
0180   71 99 c0 9b 17 fb 9d 95 eb f7 39 00 bb df e2 a7  q.........9.....
0190   48 84 21 d2 cf fe 09 3e 42 99 fa 95 da 05 2b 3a  H.!....>B.....+:
01a0   50 4b 07 08 a7 cb a5 15 28 00 00 00 1c 00 00 00  PK......(.......
01b0   50 4b 01 02 1e 03 0a 00 0b 00 00 00 78 9c 6d 47  PK..........x.mG
01c0   a7 cb a5 15 28 00 00 00 1c 00 00 00 08 00 18 00  ....(...........
01d0   00 00 00 00 01 00 00 00 a4 81 00 00 00 00 66 6c  ..............fl
01e0   61 67 2e 74 78 74 55 54 05 00 03 84 2d 46 56 75  ag.txtUT....-FVu
01f0   78 0b 00 01 04 e8 03 00 00 04 e8 03 00 00 50 4b  x.............PK
0200   05 06 00 00 00 00 01 00 01 00 4e 00 00 00 7a 00  ..........N...z.
0210   00 00 00 00                                      ....
```

This is a password-protected zip file. Now we only need to use the program `fcrackzip` and the dictionary `rockyou.txt` to get the password of the zip.

```
root@rainbowlyte:/tmp# fcrackzip -u file -D

PASSWORD FOUND!!!!: pw == azulcrema
```

We can now extract the flag of the zip archive.
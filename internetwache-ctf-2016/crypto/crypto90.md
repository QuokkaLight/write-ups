# Crypto90 - The Bank

## Description

Everyone knows that banks are insecure. This one super secure and only allows only 20 transactions per session. I always wanted a million on my account.

## Solution

We only have 20 transactions to get to the million.

When we create a transaction, we enter the amount we want to transfer and we get back a hash corresponding to that transaction. Then, to complete the transaction, we enter the transaction id and the hash. If the hash is correct, our account is credited with the amount we entered in the first command.

```
WELCOME TO THE BANK BACKEND!

Possible commands:
	help - Prints this message
	create <a> - Creates a new transaction with amount <a>
	complete <tid> <hash> - Completes a transaction to the current account. <tid> is the transaction ID to use and <hash> the verification hash.

Your balance: 0, 20 transactions left.
Command: create 100
Transaction #0 over 100 initiated. Please complete it using the verification code: 201107233b6619255504600f301e7209
Your balance: 0, 19 transactions left.
Command: complete 0 201107233b6619255504600f301e7209
Transaction completed!
Your balance: 100, 19 transactions left.
```

Let's first study how the hash are created by analyzing the function `encrypt`.

```python
def encrypt(self, t):
	self.__r.set_x(t.get_k())
	ct = ""
	s = str(t)
	l = len(s)
	for c in s:
		getnext = self.__r.get_next()
		print getnext
		print getnext % 2**7
		ct += chr( ord(c) ^ (getnext % 2**7) )
	print ct.encode('hex')
	return ct.encode('hex')
```

`t.get_k()` returns a random 32 bits hash which is used to initialize the `Randomizer` object `__r`.
Once we know the initial value of `__r` the subsequent `get_next` operations are determinists. 
The values of `__r.get_next()` are used to encrypt the message `TRANSACTION: xxxx` where `xxxx` is the amount of the transaction.

To exploit this program, we need to replace the space in the message `TRANSACTION: xxxx` by a `9`.

In order to do that, we isolate the encoded byte representing the `space` in the transaction hash and XOR it with the hexadecimal value of the `space` ascii code. 

To automate the process, I wrote this little Python script.

```python
import sys

s = sys.argv[1]

c = s[24:26].decode('hex')
x = ord(c) ^ 32
c = ord('9') ^ x
c = hex(c).lstrip("0x")

s = s[:24]  + c + s[26:]

print s
```

Now we can hack every transactions to change the amount.

```
WELCOME TO THE BANK BACKEND!

Possible commands:
	help - Prints this message
	create <a> - Creates a new transaction with amount <a>
	complete <tid> <hash> - Completes a transaction to the current account. <tid> is the transaction ID to use and <hash> the verification hash.

Your balance: 0, 20 transactions left.
Command: create 5000
Transaction #0 over 5000 initiated. Please complete it using the verification code: 58295f2b531e713d7d4c481708522a016c
Your balance: 0, 19 transactions left.
Command: complete 0 58295f2b531e713d7d4c481711522a016c
Transaction completed!
Your balance: 95000, 19 transactions left.
[...]
Command: create 5000
Transaction #11 over 5000 initiated. Please complete it using the verification code: 706137134b5649350574101f602a421944
Your balance: 950000, 8 transactions left.
Command: complete 11 706137134b5649350574101f792a421944
Transaction completed!
IW{SHUT_UP_AND_T4K3_MY_M000NEYY}
Your balance: 1045000, 8 transactions left.
```

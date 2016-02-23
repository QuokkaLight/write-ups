# Crypto90 - The Bank

## Description

My friend really can't remember passwords. So he uses some kind of obfuscation. Can you restore the plaintext?

## Solution

In the `README` file of the challenge we get the following string.

```
0000000 126 062 126 163 142 103 102 153 142 062 065 154 111 121 157 113
0000020 122 155 170 150 132 172 157 147 123 126 144 067 124 152 102 146
0000040 115 107 065 154 130 062 116 150 142 154 071 172 144 104 102 167
0000060 130 063 153 167 144 130 060 113 012
0000071
```

We notice that it's a sequence of characters in octal.
Here is the decoded string.

```
V2VsbCBkb25lIQoKRmxhZzogSVd7TjBfMG5lX2Nhbl9zdDBwX3kwdX0K
```

Now we have a string encoded in base64 that we can decode.

```
Well done!

Flag: IW{N0_0ne_can_st0p_y0u}
```
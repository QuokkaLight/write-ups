# Rev80 - Eso Tape

## Description

I once took a nap on my keyboard. I dreamed of a brand new language, but I could not decipher it nor get its meaning. Can you help me? Hint: Replace the spaces with either '{' or '}' in the solution. Hint: Interpreters don't help. Operations write to the current index.

## Solution

With a bit of research we found out that the programming language used in this challenge is called `TapeBagel`.

This is the program reversed.

```
## 		resets all of the integers to zero
%% 		resets the integer index to zero
%++ 	i[0]++
%++ 	i[0]++
%++ 	i[0] = 3
%# 		i[1]
*&* 	i[1] = 9
@** 	print i[1] -> 9 -> I
%# 		i[2]
**&* 	i[2] = i[0]*i[1] = 27
***-*	i[2] = i[2] - i[0] = 24
***-* 	i[2] = 21
%++ 	i[2]++
%++ 	i[2]++
@*** 	print i[2] -> 21 -> W
*-* 	i[2] = 0
@*** 	print i[2] -> ' ' -> {
@** 	print i[1] -> 9 -> I
*+** 	i[2] = i[1] + i[0] = 12
@*** 	print i[2] -> 12 -> L
***+* 	i[2] = i[2] + i[0] = 12 + 3 = 15
@*** 	print i[2] -> 15 -> O
**+** 	i[2] = i[1] + i[1] = 18
***+* 	i[2] = i[2] + i[0] = 21
%++ 	i[2]++
@*** 	print i[2] -> 22 -> V
#% 		sets all the integers to one
%% 		resets the integer index to zero
%++ 	i[0]++
%++ 	i[0]++
%++		i[0]++
%++		i[0]++ -> i[0] = 5
@* 		print i[0] -> 5 -> E
%# 		adds one to the integer index
%++ 	i[1]++
%++ 	i[1]++ 
%++ 	i[1]++ -> i[1] = 4
%% 		resets the integer index to zero
*&** 	i[0] = i[0] * i[1] = 20
@* 		print i[0] -> 20 -> T
@*** 	print i[2] -> 1 -> A
*-** 	i[0] = i[0] - i[1] = 16
@* 		print i[0] -> 16 -> P
%# 		adds one to the integer index
%++ 	i[1]++ -> i[1] = 5
@** 	print i[1] -> 5 -> E
*-** 	i[1] = i[0] - i[1] = 11
*-** 	i[1] = i[0] - i[1] = 5
**-*** i[1] = i[1] - i[2] = 4
**-*** i[1] = i[1] - i[2] = 3
**-*** i[1] = i[1] - i[2] = 2
@** 	print i[1] -> 2 -> B
@*** 	print i[2] -> 1 -> A
#% 		sets all the integers to one
%% 		resets the integer index to zero
%++ 	i[0]++
%++		i[0]++
%++		i[0]++
%++		i[0]++ -> i[0] = 5
%# 		adds one to the integer index
*+** 	i[1] = i[0] + i[1] = 6
%++ 	i[1]++ -> i[1] = 7
@** 	print i[1] -> 7 -> G
@* 		print i[0] -> 5 -> E
%# 		adds one to the integer index
*+** 	i[2] = i[0] + i[1] = 12
@*** 	print i[2] -> 12 -> L
## 		resets all of the integers to zero
%%		resets the integer index to zero
@***	print i[2] -> 0 -> ' '
```

In the end, ~~it doesn't even~~ the flag is `IW{ILOVETAPEBAGEL}`
# Sec-Coding 1

## Task

You should fix vulnerabilities of the given source code, WITHOUT changing its normal behaviour.

**Rules & Notes**

 * MISSION: You should fix vulnerabilities of the given source code, WITHOUT changing its normal behaviour.
 * RULE0: When an honest user gives a non-malicious (but maybe incorrect) input which does not trigger the vulnerabilities,
the output of uploaded fixed code should be the same as before.
 * RULE1: When the attacker gives his/her attack vector, your program should not crash or do dangerous actions (explained below),
but continue its execution and exit normally at the end. In this situation, your program is allowed to output anything.
 * RULE2: A (poorly-tested) source code may crash even when interacting with a normal user. You should fix these cases too.
(NOTE: the output should be correct in this case)
 * Dangerous actions (stated above) includes buffer overflows, writing to unallocated memory address, reading uninitialized memory,
and any other programming mistakes leading to crash/instability.
 * Some prevention techniques, detect the attack and prevent memory corruption but throw an exception which terminates the program,
leading to denial of service. You should avoid such termination and the program should recover from the attack, continue execution,
and exit normally at the end.

## Vulnerable source code

```c

#include <vector>
#include <iostream>
#include <windows.h>

using namespace std;


int main()
{
	vector<char> str(MAX_PATH);
	
	cout << "Enter your name: ";
	cin >> str.data();

	cout << "Hello " << str.data() << " :)" << endl;

	return -14;
}
```

## Solution

```c
#include <vector>
#include <iostream>
#include <windows.h>

using namespace std;


int main()
{
	char str[MAX_PATH];
	
	cout << "Enter your name: ";
	cin.get(str, MAX_PATH);

	cout << "Hello " << str << " :)" << endl;

	return -14;
}
```
# Sec-Coding 2

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

#include <math.h>
#include <stdio.h>
#include <windows.h>


int main(int argc, char **argv)
{
	// STRING ECHO
	//
	// Sample usage:
	//   strecho repeat=4,str=pleaseechome

	char *str = (char *)malloc(100);
	int repeat = 0;

	char *line = GetCommandLineA();

	while (*line != ' ')
		line++;
	line++;

	if (strncmp(line, "repeat=", 7) == 0)
	{
		line += 7;
		repeat = atoi(line);
		line += (int)ceil(log10((double)repeat)) + 1;
	}

	if (strncmp(line, "str=", 4) == 0)
	{
		line += 4;
		str = strtok(line, " ");
	}

	for (int i = 0; i < repeat; i++)
		printf("%s\n", str);

	line += strlen(str);
	for (; line >= GetCommandLineA(); line--)
		*line = '\x0';

	free(str);

	return -14;
}
```

## Solution

```c

#include <math.h>
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <windows.h>


int main(int argc, char **argv)
{
	int i = 0;
	int j = 0;

	char str[100];
	char str2[100];
	int repeat = 0;

	// char *line = argv[1];
	char *line = GetCommandLineA();
	char *line_ptr = line;
	char *str_ptr = str;
	int line_size = strlen(line);

	char *repeateq;
	char *streq;

	repeateq = strstr(line, "repeat=");

	if (repeateq != NULL) {
		repeateq += 7;
		repeat = strtol(repeateq, NULL, 10);
		
		if(repeat > 0) {
			streq = strstr(repeateq, "str=");

			if (streq != NULL) {
				str_ptr = streq;

				for (i = 0; i < repeat; i++)
					printf("%s\n", streq+4);
			} else {
				printf("nope\n");
			}
		}
		else {
			printf("nope\n");
		}
	}
	else {
		printf("nope\n");
	}

	return -14;
}
```
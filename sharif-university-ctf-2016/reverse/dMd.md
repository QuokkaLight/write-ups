# dMd

## Task

Flag is : The valid input

## Solution

We used `radare` to analyze the executable.

```bash
rainbowlyte@ns38534:/tmp$ radare2 dMd
 -- "a collection of garbage" -- an r2 pro user
[0x00400da0]> aa
[0x00400da0]> pdf @ main
            ;-- main:
╒ (fcn) sym.main 1342
│           ; var int local_0_1    @ rbp-0x1
│           ; var int local_3      @ rbp-0x18
│           ; var int local_10     @ rbp-0x50
│           ; var int local_11     @ rbp-0x58
│           ; var int local_12     @ rbp-0x60
│           ; var int local_14     @ rbp-0x70
│           ; var int local_14_1   @ rbp-0x71
│           ; DATA XREF from 0x00400dbd (sym.main)
│           0x00400e8d      55             push rbp
│           0x00400e8e      4889e5         mov rbp, rsp
│           0x00400e91      53             push rbx
│           0x00400e92      4883ec78       sub rsp, 0x78

[...]

│           0x00400f36      3c37           cmp al, 0x37                ; '7'
│       ┌─< 0x00400f38      0f855d030000   jne 0x40129b
│       │   0x00400f3e      488b45a8       mov rax, qword [rbp-local_11]
│       │   0x00400f42      4883c001       add rax, 1
│       │   0x00400f46      0fb600         movzx eax, byte [rax]
│       │   0x00400f49      3c38           cmp al, 0x38                ; '8'
│      ┌──< 0x00400f4b      0f854a030000   jne 0x40129b
│      ││   0x00400f51      488b45a8       mov rax, qword [rbp-local_11]
│      ││   0x00400f55      4883c002       add rax, 2
│      ││   0x00400f59      0fb600         movzx eax, byte [rax]
│      ││   0x00400f5c      3c30           cmp al, 0x30                ; '0'
│     ┌───< 0x00400f5e      0f8537030000   jne 0x40129b
│     │││   0x00400f64      488b45a8       mov rax, qword [rbp-local_11]
│     │││   0x00400f68      4883c003       add rax, 3
│     │││   0x00400f6c      0fb600         movzx eax, byte [rax]
│     │││   0x00400f6f      3c34           cmp al, 0x34                ; '4'
│    ┌────< 0x00400f71      0f8524030000   jne 0x40129b
│    ││││   0x00400f77      488b45a8       mov rax, qword [rbp-local_11]
│    ││││   0x00400f7b      4883c004       add rax, 4
│    ││││   0x00400f7f      0fb600         movzx eax, byte [rax]
│    ││││   0x00400f82      3c33           cmp al, 0x33                ; '3'
│   ┌─────< 0x00400f84      0f8511030000   jne 0x40129b
│   │││││   0x00400f8a      488b45a8       mov rax, qword [rbp-local_11]
│   │││││   0x00400f8e      4883c005       add rax, 5
│   │││││   0x00400f92      0fb600         movzx eax, byte [rax]
│   │││││   0x00400f95      3c38           cmp al, 0x38                ; '8'
│  ┌──────< 0x00400f97      0f85fe020000   jne 0x40129b
│  ││││││   0x00400f9d      488b45a8       mov rax, qword [rbp-local_11]
│  ││││││   0x00400fa1      4883c006       add rax, 6
│  ││││││   0x00400fa5      0fb600         movzx eax, byte [rax]
│  ││││││   0x00400fa8      3c64           cmp al, 0x64                ; 'd'
│ ┌───────< 0x00400faa      0f85eb020000   jne 0x40129b
│ │││││││   0x00400fb0      488b45a8       mov rax, qword [rbp-local_11]
│ │││││││   0x00400fb4      4883c007       add rax, 7
│ │││││││   0x00400fb8      0fb600         movzx eax, byte [rax]
│ │││││││   0x00400fbb      3c35           cmp al, 0x35                ; '5'
│ ────────< 0x00400fbd      0f85d8020000   jne 0x40129b
│ │││││││   0x00400fc3      488b45a8       mov rax, qword [rbp-local_11]
│ │││││││   0x00400fc7      4883c008       add rax, 8
│ │││││││   0x00400fcb      0fb600         movzx eax, byte [rax]
│ │││││││   0x00400fce      3c62           cmp al, 0x62                ; 'b'
│ ────────< 0x00400fd0      0f85c5020000   jne 0x40129b
│ │││││││   0x00400fd6      488b45a8       mov rax, qword [rbp-local_11]
│ │││││││   0x00400fda      4883c009       add rax, 9
│ │││││││   0x00400fde      0fb600         movzx eax, byte [rax]
│ │││││││   0x00400fe1      3c36           cmp al, 0x36                ; '6'
│ ────────< 0x00400fe3      0f85b2020000   jne 0x40129b
│ │││││││   0x00400fe9      488b45a8       mov rax, qword [rbp-local_11]
│ │││││││   0x00400fed      4883c00a       add rax, 0xa
│ │││││││   0x00400ff1      0fb600         movzx eax, byte [rax]
│ │││││││   0x00400ff4      3c65           cmp al, 0x65                ; 'e'
│ ────────< 0x00400ff6      0f859f020000   jne 0x40129b
│ │││││││   0x00400ffc      488b45a8       mov rax, qword [rbp-local_11]
│ │││││││   0x00401000      4883c00b       add rax, 0xb
│ │││││││   0x00401004      0fb600         movzx eax, byte [rax]
│ │││││││   0x00401007      3c32           cmp al, 0x32                ; '2'
│ ────────< 0x00401009      0f858c020000   jne 0x40129b
│ │││││││   0x0040100f      488b45a8       mov rax, qword [rbp-local_11]
│ │││││││   0x00401013      4883c00c       add rax, 0xc
│ │││││││   0x00401017      0fb600         movzx eax, byte [rax]
│ │││││││   0x0040101a      3c39           cmp al, 0x39                ; '9'
│ ────────< 0x0040101c      0f8579020000   jne 0x40129b
│ │││││││   0x00401022      488b45a8       mov rax, qword [rbp-local_11]
│ │││││││   0x00401026      4883c00d       add rax, 0xd
│ │││││││   0x0040102a      0fb600         movzx eax, byte [rax]
│ │││││││   0x0040102d      3c64           cmp al, 0x64                ; 'd'
│ ────────< 0x0040102f      0f8566020000   jne 0x40129b
│ │││││││   0x00401035      488b45a8       mov rax, qword [rbp-local_11]
│ │││││││   0x00401039      4883c00e       add rax, 0xe
│ │││││││   0x0040103d      0fb600         movzx eax, byte [rax]
│ │││││││   0x00401040      3c62           cmp al, 0x62                ; 'b'
│ ────────< 0x00401042      0f8553020000   jne 0x40129b
│ │││││││   0x00401048      488b45a8       mov rax, qword [rbp-local_11]
│ │││││││   0x0040104c      4883c00f       add rax, 0xf
│ │││││││   0x00401050      0fb600         movzx eax, byte [rax]
│ │││││││   0x00401053      3c30           cmp al, 0x30                ; '0'
│ ────────< 0x00401055      0f8540020000   jne 0x40129b
│ │││││││   0x0040105b      488b45a8       mov rax, qword [rbp-local_11]
│ │││││││   0x0040105f      4883c010       add rax, 0x10
│ │││││││   0x00401063      0fb600         movzx eax, byte [rax]
│ │││││││   0x00401066      3c38           cmp al, 0x38                ; '8'
│ ────────< 0x00401068      0f852d020000   jne 0x40129b
│ │││││││   0x0040106e      488b45a8       mov rax, qword [rbp-local_11]
│ │││││││   0x00401072      4883c011       add rax, 0x11
│ │││││││   0x00401076      0fb600         movzx eax, byte [rax]
│ │││││││   0x00401079      3c39           cmp al, 0x39                ; '9'
│ ────────< 0x0040107b      0f851a020000   jne 0x40129b
│ │││││││   0x00401081      488b45a8       mov rax, qword [rbp-local_11]
│ │││││││   0x00401085      4883c012       add rax, 0x12
│ │││││││   0x00401089      0fb600         movzx eax, byte [rax]
│ │││││││   0x0040108c      3c38           cmp al, 0x38                ; '8'
│ ────────< 0x0040108e      0f8507020000   jne 0x40129b
│ │││││││   0x00401094      488b45a8       mov rax, qword [rbp-local_11]
│ │││││││   0x00401098      4883c013       add rax, 0x13
│ │││││││   0x0040109c      0fb600         movzx eax, byte [rax]
│ │││││││   0x0040109f      3c62           cmp al, 0x62                ; 'b'
│ ────────< 0x004010a1      0f85f4010000   jne 0x40129b
│ │││││││   0x004010a7      488b45a8       mov rax, qword [rbp-local_11]
│ │││││││   0x004010ab      4883c014       add rax, 0x14
│ │││││││   0x004010af      0fb600         movzx eax, byte [rax]
│ │││││││   0x004010b2      3c63           cmp al, 0x63                ; 'c'
│ ────────< 0x004010b4      0f85e1010000   jne 0x40129b
│ │││││││   0x004010ba      488b45a8       mov rax, qword [rbp-local_11]
│ │││││││   0x004010be      4883c015       add rax, 0x15
│ │││││││   0x004010c2      0fb600         movzx eax, byte [rax]
│ │││││││   0x004010c5      3c34           cmp al, 0x34                ; '4'
│ ────────< 0x004010c7      0f85ce010000   jne 0x40129b
│ │││││││   0x004010cd      488b45a8       mov rax, qword [rbp-local_11]
│ │││││││   0x004010d1      4883c016       add rax, 0x16
│ │││││││   0x004010d5      0fb600         movzx eax, byte [rax]
│ │││││││   0x004010d8      3c66           cmp al, 0x66                ; 'f'
│ ────────< 0x004010da      0f85bb010000   jne 0x40129b
│ │││││││   0x004010e0      488b45a8       mov rax, qword [rbp-local_11]
│ │││││││   0x004010e4      4883c017       add rax, 0x17
│ │││││││   0x004010e8      0fb600         movzx eax, byte [rax]
│ │││││││   0x004010eb      3c30           cmp al, 0x30                ; '0'
│ ────────< 0x004010ed      0f85a8010000   jne 0x40129b
│ │││││││   0x004010f3      488b45a8       mov rax, qword [rbp-local_11]
│ │││││││   0x004010f7      4883c018       add rax, 0x18
│ │││││││   0x004010fb      0fb600         movzx eax, byte [rax]
│ │││││││   0x004010fe      3c32           cmp al, 0x32                ; '2'
│ ────────< 0x00401100      0f8595010000   jne 0x40129b
│ │││││││   0x00401106      488b45a8       mov rax, qword [rbp-local_11]
│ │││││││   0x0040110a      4883c019       add rax, 0x19
│ │││││││   0x0040110e      0fb600         movzx eax, byte [rax]
│ │││││││   0x00401111      3c32           cmp al, 0x32                ; '2'
│ ────────< 0x00401113      0f8582010000   jne 0x40129b
│ │││││││   0x00401119      488b45a8       mov rax, qword [rbp-local_11]
│ │││││││   0x0040111d      4883c01a       add rax, 0x1a
│ │││││││   0x00401121      0fb600         movzx eax, byte [rax]
│ │││││││   0x00401124      3c35           cmp al, 0x35                ; '5'
│ ────────< 0x00401126      0f856f010000   jne 0x40129b
│ │││││││   0x0040112c      488b45a8       mov rax, qword [rbp-local_11]
│ │││││││   0x00401130      4883c01b       add rax, 0x1b
│ │││││││   0x00401134      0fb600         movzx eax, byte [rax]
│ │││││││   0x00401137      3c39           cmp al, 0x39                ; '9'
│ ────────< 0x00401139      0f855c010000   jne 0x40129b
│ │││││││   0x0040113f      488b45a8       mov rax, qword [rbp-local_11]
│ │││││││   0x00401143      4883c01c       add rax, 0x1c
│ │││││││   0x00401147      0fb600         movzx eax, byte [rax]
│ │││││││   0x0040114a      3c33           cmp al, 0x33                ; '3'
│ ────────< 0x0040114c      0f8549010000   jne 0x40129b
│ │││││││   0x00401152      488b45a8       mov rax, qword [rbp-local_11]
│ │││││││   0x00401156      4883c01d       add rax, 0x1d
│ │││││││   0x0040115a      0fb600         movzx eax, byte [rax]
│ │││││││   0x0040115d      3c35           cmp al, 0x35                ; '5'
│ ────────< 0x0040115f      0f8536010000   jne 0x40129b
│ │││││││   0x00401165      488b45a8       mov rax, qword [rbp-local_11]
│ │││││││   0x00401169      4883c01e       add rax, 0x1e
│ │││││││   0x0040116d      0fb600         movzx eax, byte [rax]
│ │││││││   0x00401170      3c63           cmp al, 0x63                ; 'c'
│ ────────< 0x00401172      0f8523010000   jne 0x40129b
│ │││││││   0x00401178      488b45a8       mov rax, qword [rbp-local_11]
│ │││││││   0x0040117c      4883c01f       add rax, 0x1f
│ │││││││   0x00401180      0fb600         movzx eax, byte [rax]
│ │││││││   0x00401183      3c30           cmp al, 0x30                ; '0'
│ ────────< 0x00401185      0f8510010000   jne 0x40129b

[...]

│      └──> 0x004013bf      e85cf9ffff     call sym.imp.__stack_chk_fail
│       └─> 0x004013c4      4883c478       add rsp, 0x78
│           0x004013c8      5b             pop rbx
│           0x004013c9      5d             pop rbp
╘           0x004013ca      c3             ret
[0x00400da0]>
```

There are 32 comparison to check if the string is `780438d5b6e29db0898bc4f0225935c0` which is the double md5 of `grape` (`md5(md5(grape)) = 780438d5b6e29db0898bc4f0225935c0 `).

The function `_Z3md5Ss` called prior to the comparisons led us to believe that the correct key is the md5 hash of `grape`. Which is true.

```bash
rainbowlyte@ns38534:/tmp$ ./dMd
Enter the valid key!
b781cbb29054db12f88f08c6e161c199
The key is valid :)
```



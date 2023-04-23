## Binary Bomb Phase 1 (50 Points)


### Problem
```
Starting off with small strings...

Same Files For All Binary Bomb

You may enter SKIP to skip a phase or HELP to access the help menu 
```

### Solution
I used the tool Radare2 to solve this challenge

First I loaded the bomb into Radare2 and analyzed it

```
$r2 dawg_bbomb
[0x00002310]> aaa
...
```
Then I looked for the different phases of the bomb

```
[0x00002310]>afl~phase
0x000026c5    8    144 sym.phase2
0x0000294c   14    388 sym.phase4
0x000034bd   10    188 sym.phase8
0x00002d0c   20    507 sym.phase6
0x0000266f    5     86 sym.phase1
0x00003579   14    640 sym.phase9
0x0000285a    8    242 sym.phase3
0x00002feb   12    774 sym.phase7
0x00002ad0   15    572 sym.phase5
0x000037f9    9    382 sym.phasePass
0x00003977   14    544 sym.phaseFail
...
```
Finally I looked at `sym.phase1` to find the password to the fist phase of the bomb

```
[0x00002310]>s sym.phase1
[0x0000266f]>pdf
            ; DATA XREF from main @ 0x486d(r)
┌ 86: sym.phase1 (char *arg1, size_t arg2);
│           ; arg char *arg1 @ rdi
│           ; arg size_t arg2 @ rsi
│           ; var char *s2 @ rbp-0x8
│           ; var char *s1 @ rbp-0x18
│           ; var size_t n @ rbp-0x20
│           0x0000266f      55             push rbp
│           0x00002670      4889e5         mov rbp, rsp
│           0x00002673      4883ec20       sub rsp, 0x20
│           0x00002677      48897de8       mov qword [s1], rdi         ; arg1
│           0x0000267b      488975e0       mov qword [n], rsi          ; arg2
│           0x0000267f      488d05562b00.  lea rax, str.BabYs_F1rS7_RE ; 0x51dc ; "BabYs_F1rS7_RE"
│           0x00002686      488945f8       mov qword [s2], rax
│           0x0000268a      488b55e0       mov rdx, qword [n]          ; size_t n
│           0x0000268e      488b4df8       mov rcx, qword [s2]
│           0x00002692      488b45e8       mov rax, qword [s1]
│           0x00002696      4889ce         mov rsi, rcx                ; const char *s2
│           0x00002699      4889c7         mov rdi, rax                ; const char *s1
│           0x0000269c      e8dff9ffff     call sym.imp.strncmp        ; int strncmp(const char *s1, const char *s2, size_t n)
│           0x000026a1      85c0           test eax, eax
│       ┌─< 0x000026a3      7512           jne 0x26b7
│       │   0x000026a5      488b45f8       mov rax, qword [s2]
│       │   0x000026a9      4889c7         mov rdi, rax                ; const char *s
│       │   0x000026ac      e81ffaffff     call sym.imp.strlen         ; size_t strlen(const char *s)
│       │   0x000026b1      483945e0       cmp qword [n], rax
│      ┌──< 0x000026b5      7407           je 0x26be
│      ││   ; CODE XREF from sym.phase1 @ 0x26a3(x)
│      │└─> 0x000026b7      b801000000     mov eax, 1
│      │┌─< 0x000026bc      eb05           jmp 0x26c3
│      ││   ; CODE XREF from sym.phase1 @ 0x26b5(x)
│      └──> 0x000026be      b800000000     mov eax, 0
│       │   ; CODE XREF from sym.phase1 @ 0x26bc(x)
│       └─> 0x000026c3      c9             leave
└           0x000026c4      c3             ret
...
```
The password was very clear from here, so I put it into the first phase of the bomb to get the flag


Flag = `DawgCTF{BabYs_F1rS7_RE}`
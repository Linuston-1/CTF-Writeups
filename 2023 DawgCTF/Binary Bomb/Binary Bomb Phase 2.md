## Challenge Title ( Points)


### Problem
```
Can you help me? I lost my key and can't read my string.
```

### Solution
Please reference Binary Bomb Phase 1 for the steps to get into the Binary Bomb


I stared off just like phase 1 and took a look at `sym.phase2`

```
[0x00002310]> pdf@sym.phase2
            ; DATA XREF from main @ 0x487b(r)
┌ 144: sym.phase2 (char *arg1, size_t arg2);
│           ; arg char *arg1 @ rdi
│           ; arg size_t arg2 @ rsi
│           ; var char *s2 @ rbp-0x8
│           ; var int64_t var_ch @ rbp-0xc
│           ; var char *s1 @ rbp-0x18
│           ; var size_t n @ rbp-0x20
│           0x000026c5      55             push rbp
│           0x000026c6      4889e5         mov rbp, rsp
│           0x000026c9      4883ec20       sub rsp, 0x20
│           0x000026cd      48897de8       mov qword [s1], rdi         ; arg1
│           0x000026d1      488975e0       mov qword [n], rsi          ; arg2
│           0x000026d5      488d050f2b00.  lea rax, str._agbVPfVO9VA:ey8gn ; 0x51eb ; "]a=gbVPf\VO9{VA:ey8gn"
│           0x000026dc      488945f8       mov qword [s2], rax
│           0x000026e0      c745f4000000.  mov dword [var_ch], 0
│       ┌─< 0x000026e7      eb26           jmp 0x270f
│       │   ; CODE XREF from sym.phase2 @ 0x2718(x)
│      ┌──> 0x000026e9      8b45f4         mov eax, dword [var_ch]
│      ╎│   0x000026ec      4863d0         movsxd rdx, eax
│      ╎│   0x000026ef      488b45e8       mov rax, qword [s1]
│      ╎│   0x000026f3      4801d0         add rax, rdx
│      ╎│   0x000026f6      0fb610         movzx edx, byte [rax]
│      ╎│   0x000026f9      8b45f4         mov eax, dword [var_ch]
│      ╎│   0x000026fc      4863c8         movsxd rcx, eax
│      ╎│   0x000026ff      488b45e8       mov rax, qword [s1]
│      ╎│   0x00002703      4801c8         add rax, rcx
│      ╎│   0x00002706      83f209         xor edx, 9
│      ╎│   0x00002709      8810           mov byte [rax], dl
│      ╎│   ; DATA XREF from sym.explodeTwo @ 0x3f6e(r)
│      ╎│   0x0000270b      8345f401       add dword [var_ch], 1
│      ╎│   ; CODE XREF from sym.phase2 @ 0x26e7(x)
│      ╎└─> 0x0000270f      8b45f4         mov eax, dword [var_ch]
│      ╎    0x00002712      4898           cdqe
│      ╎    0x00002714      483b45e0       cmp rax, qword [n]
│      └──< 0x00002718      72cf           jb 0x26e9
│           0x0000271a      488b55e0       mov rdx, qword [n]          ; size_t n
│           0x0000271e      488b4df8       mov rcx, qword [s2]
│           0x00002722      488b45e8       mov rax, qword [s1]
│           0x00002726      4889ce         mov rsi, rcx                ; const char *s2
│           0x00002729      4889c7         mov rdi, rax                ; const char *s1
│           0x0000272c      e84ff9ffff     call sym.imp.strncmp        ; int strncmp(const char *s1, const char *s2, size_t n)
│           0x00002731      85c0           test eax, eax
│       ┌─< 0x00002733      7512           jne 0x2747
│       │   0x00002735      488b45f8       mov rax, qword [s2]
│       │   0x00002739      4889c7         mov rdi, rax                ; const char *s
│       │   0x0000273c      e88ff9ffff     call sym.imp.strlen         ; size_t strlen(const char *s)
│       │   0x00002741      483945e0       cmp qword [n], rax
│      ┌──< 0x00002745      7407           je 0x274e
│      ││   ; CODE XREF from sym.phase2 @ 0x2733(x)
│      │└─> 0x00002747      b801000000     mov eax, 1
│      │┌─< 0x0000274c      eb05           jmp 0x2753
│      ││   ; CODE XREF from sym.phase2 @ 0x2745(x)
│      └──> 0x0000274e      b800000000     mov eax, 0
│       │   ; CODE XREF from sym.phase2 @ 0x274c(x)
│       └─> 0x00002753      c9             leave
└           0x00002754      c3             ret
...
```
In the same spot as the last flag there is another string of text, but it appears to be encoded

I tried using the [Cipher Identifier](https://www.dcode.fr/cipher-identifier) on Dcode.fr, but it did not give me any results

I then turned to [Cyberchef](https://gchq.github.io/CyberChef/#recipe=Magic(3,true,false,'')&input=XWE9Z2JWUGZcVk85e1ZBOmV5OGdu) and used the `Magic` operator to try and automatically decrypt the string

This revealed that the string was XOR encoded

After I got the password, I put it into the binary to get the flag


Flag = `DawgCTF{Th4nk_YoU_F0r_H3lp1ng}`
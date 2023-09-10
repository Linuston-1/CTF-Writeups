## Patchwork


### Problem
```
This program should just give the flag, but I set the wrong value in the code and now it refuses to jump to the correct function. Could you patch it for me?

Flag format: PCTF{}

Author: @necktie5740
```
Files provided:
- patchwork
### Solution

We are given a binary file patchwork. My preferred reverse engineering tool is [Radare 2](https://rada.re/n/).

To begin with I start with some preliminary steps:

1. Load up the file into Radare2 and analyze it.
```bash
$ r2 patchwork
WARN: run r2 with -e bin.cache=true to fix relocations in disassembly
 -- Use 'zoom.byte=printable' in zoom mode ('z' in Visual mode) to find strings
[0x00001050]> aaaa

(Output Omited)

```

2. List all of the functions in the binary.
```bash
[0x00001050]> afl
0x00001050    1     33 entry0
0x00001080    4     34 sym.deregister_tm_clones
0x000010b0    4     51 sym.register_tm_clones
0x000010f0    5     54 sym.__do_global_dtors_aux
0x00001040    1      6 sym.imp.__cxa_finalize
0x00001130    1      9 sym.frame_dummy
0x0000121c    1      9 sym._fini
0x0000117d    7    157 sym.give_flag
0x00001139    3     68 main
0x00001030    1      6 sym.imp.puts
0x00001000    3     23 sym._init
[0x00001050]>

```

**main** and **sym.give_flag** are the functions of interest.

3. Start by analyzing the decompliation of **main**
```bash
[0x00001050]> pdf@main
            ; DATA XREF from entry0 @ 0x1064(r)
┌ 68: int main (int argc, char **argv, char **envp);
│           ; var uint32_t var_4h @ rbp-0x4
│           0x00001139      55             push rbp
│           0x0000113a      4889e5         mov rbp, rsp
│           0x0000113d      4883ec10       sub rsp, 0x10
│           0x00001141      c745fc000000.  mov dword [var_4h], 0
│           0x00001148      488d05b90e00.  lea rax, str.Trampolines_are_quite_fun___I_love_to_jump__ ; 0x2008 ; "Trampolines are quite fun!; I love to jump! "
│           0x0000114f      4889c7         mov rdi, rax                ; const char *s
│           0x00001152      e8d9feffff     call sym.imp.puts           ; int puts(const char *s)
│           0x00001157      488d05da0e00.  lea rax, str.You_should_try_jumping_too__Itll_sure_be_more_fun_than_reversing_the_flag_manually. ; 0x2038 ; "You should try jumping too! It'll sure be more fun than reversing the flag manually."
│           0x0000115e      4889c7         mov rdi, rax                ; const char *s
│           0x00001161      e8cafeffff     call sym.imp.puts           ; int puts(const char *s)
│           0x00001166      837dfc00       cmp dword [var_4h], 0
│       ┌─< 0x0000116a      740a           je 0x1176
│       │   0x0000116c      b800000000     mov eax, 0
│       │   0x00001171      e807000000     call sym.give_flag
│       │   ; CODE XREF from main @ 0x116a(x)
│       └─> 0x00001176      b800000000     mov eax, 0
│           0x0000117b      c9             leave
└           0x0000117c      c3             ret
[0x00001050]>
```

We can see that there is a jump operation that skips over the **sym.give_flag** function.

We can also check the **sym.give_flag** function to see if the flag is listed in plaintext for us to easily grab.

```bash
[0x00001050]> pdf@sym.give_flag
            ; CALL XREF from main @ 0x1171(x)
┌ 157: sym.give_flag ();
│           ; var int64_t var_8h @ rbp-0x8
│           ; var int64_t var_10h @ rbp-0x10
│           ; var int64_t var_16h @ rbp-0x16
│           ; var int64_t var_18h @ rbp-0x18
│           ; var int64_t var_20h @ rbp-0x20
│           ; var int64_t var_28h @ rbp-0x28
│           ; var char *s @ rbp-0x30
│           0x0000117d      55             push rbp
│           0x0000117e      4889e5         mov rbp, rsp
│           0x00001181      4883ec30       sub rsp, 0x30
│           0x00001185      48b8a093a496.  movabs rax, 0x9dc59acb96a493a0
│           0x0000118f      48bac0afc5a0.  movabs rdx, 0xb4be84afa0c5afc0
│           0x00001199      488945d0       mov qword [s], rax
│           0x0000119d      488955d8       mov qword [var_28h], rdx
│           0x000011a1      48b8afb783c4.  movabs rax, 0xa780b4afc483b7af
│           0x000011ab      488945e0       mov qword [var_20h], rax
│           0x000011af      66c745e8becd   mov word [var_18h], 0xcdbe
│           0x000011b5      c645ea00       mov byte [var_16h], 0
│           0x000011b9      488d45d0       lea rax, [s]
│           0x000011bd      488945f8       mov qword [var_8h], rax
│       ┌─< 0x000011c1      eb14           jmp 0x11d7
│       │   ; CODE XREF from sym.give_flag @ 0x11e0(x)
│      ┌──> 0x000011c3      488b45f8       mov rax, qword [var_8h]
│      ╎│   0x000011c7      488d5001       lea rdx, [rax + 1]
│      ╎│   0x000011cb      488955f8       mov qword [var_8h], rdx
│      ╎│   0x000011cf      0fb610         movzx edx, byte [rax]
│      ╎│   0x000011d2      83ea50         sub edx, 0x50
│      ╎│   0x000011d5      8810           mov byte [rax], dl
│      ╎│   ; CODE XREF from sym.give_flag @ 0x11c1(x)
│      ╎└─> 0x000011d7      488b45f8       mov rax, qword [var_8h]
│      ╎    0x000011db      0fb600         movzx eax, byte [rax]
│      ╎    0x000011de      84c0           test al, al
│      └──< 0x000011e0      75e1           jne 0x11c3
│           0x000011e2      488d45d0       lea rax, [s]
│           0x000011e6      4889c7         mov rdi, rax                ; const char *s
│           0x000011e9      e842feffff     call sym.imp.puts           ; int puts(const char *s)
│           0x000011ee      488d45d0       lea rax, [s]
│           0x000011f2      488945f0       mov qword [var_10h], rax
│       ┌─< 0x000011f6      eb14           jmp 0x120c
│      ┌──> 0x000011f8      488b45f0       mov rax, qword [var_10h]
│      ╎│   0x000011fc      488d5001       lea rdx, [rax + 1]
│      ╎│   0x00001200      488955f0       mov qword [var_10h], rdx
│      ╎│   0x00001204      0fb610         movzx edx, byte [rax]
│      ╎│   0x00001207      83c250         add edx, 0x50
│      ╎│   0x0000120a      8810           mov byte [rax], dl
│      ╎│   ; CODE XREF from sym.give_flag @ 0x11f6(x)
│      ╎└─> 0x0000120c      488b45f0       mov rax, qword [var_10h]
│      ╎    0x00001210      0fb600         movzx eax, byte [rax]
│      ╎    0x00001213      84c0           test al, al
│      └──< 0x00001215      75e1           jne 0x11f8
│           0x00001217      90             nop
│           0x00001218      c9             leave
└           0x00001219      c3             ret
[0x00001050]>
```

It is not. It will be easier to patch the **main** function than it will be to reverse engineer the **sym.give_flag** function

There are also hints in both the challenge description and binary itself that pushes us in this direction.


Luckily, patching a binary in Radare2 is very easy.

1. Go to the value you want to edit.

This can be done with with the `s` command.
We want to patch the jump operation that skips over the **sym.give_flag**. We already know the value is 0x0000116a
```bash
[0x00001050]> s 0x116a
[0x0000116a]>
```

2. Enter write mode

```bash
[0x0000116a]> oo+
[0x0000116a]>
```

3. Overwrite the jump operation

I do this by using the nop operation, which does nothing. This could also be done by rewriting the jump operation to the value that the **sym.give_flag** is on.

```bash
[0x0000116a]> wao nop
[0x0000116a]>
```


The binary is now patched. This can be verified by decompiling the main function again.

```bash
[0x0000116a]> pdf@main
            ; DATA XREF from entry0 @ 0x1064(r)
┌ 68: int main (int argc, char **argv, char **envp);
│           ; var uint32_t var_4h @ rbp-0x4
│           0x00001139      55             push rbp
│           0x0000113a      4889e5         mov rbp, rsp
│           0x0000113d      4883ec10       sub rsp, 0x10
│           0x00001141      c745fc000000.  mov dword [var_4h], 0
│           0x00001148      488d05b90e00.  lea rax, str.Trampolines_are_quite_fun___I_love_to_jump__ ; 0x2008 ; "Trampolines are quite fun!; I love to jump! "
│           0x0000114f      4889c7         mov rdi, rax                ; const char *s
│           0x00001152      e8d9feffff     call sym.imp.puts           ; int puts(const char *s)
│           0x00001157      488d05da0e00.  lea rax, str.You_should_try_jumping_too__Itll_sure_be_more_fun_than_reversing_the_flag_manually. ; 0x2038 ; "You should try jumping too! It'll sure be more fun than reversing the flag manually."
│           0x0000115e      4889c7         mov rdi, rax                ; const char *s
│           0x00001161      e8cafeffff     call sym.imp.puts           ; int puts(const char *s)
│           0x00001166      837dfc00       cmp dword [var_4h], 0
│           0x0000116a      90             nop
..
│           0x0000116c      b800000000     mov eax, 0
│           0x00001171      e807000000     call sym.give_flag
│           ; CODE XREF from main @ 0x116a(x)
│           0x00001176      b800000000     mov eax, 0
│           0x0000117b      c9             leave
└           0x0000117c      c3             ret
[0x0000116a]>
```

Now all that is left is to run the patched binary

```
$ ./patchwork 
Trampolines are quite fun!; I love to jump! 
You should try jumping too! It'll sure be more fun than reversing the flag manually.
PCTF{JuMp_uP_4nd_g3t_d0Wn}
```


Flag = `PCTF{JuMp_uP_4nd_g3t_d0Wn}`


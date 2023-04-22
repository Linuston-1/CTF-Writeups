## String Things (75 Points)

</br>

### Problem
```
I got this binary file called "secrets", and I really wanna know whats in it. But it asks me for a password, and I have no idea what it is! Maybe you can figure it out?
```

### Solution
We are asked to find the password to the binary file **secrets**

This can be done by using the tool rabin2 
the command `rabin2 -z secrets` yields the following:

```
nth paddr      vaddr      len size section type  string
―――――――――――――――――――――――――――――――――――――――――――――――――――――――
0   0x00000a20 0x00400a20 64  65   .rodata ascii ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/
1   0x00000a70 0x00400a70 30  31   .rodata ascii RGF3Z0NURntzdHIxbmc1X3cxbmc1fQ
2   0x00000a90 0x00400a90 19  20   .rodata ascii supers3cr3tpassword
3   0x00000aa4 0x00400aa4 20  21   .rodata ascii Enter the password:
4   0x00000abb 0x00400abb 29  30   .rodata ascii You did it!\n The flag is: %s\n
5   0x00000ae0 0x00400ae0 30  31   .rodata ascii Incorrect password. Try again.
```
By analyzing the results we can see that `supers3cr3tpassword` is likely the password it wants

Once we run the binary and input the password we get the flag

Flag: `DawgCTF{Im not posting this yet}`


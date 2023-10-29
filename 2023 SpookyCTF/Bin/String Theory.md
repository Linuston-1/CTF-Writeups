## String Theory


### Problem
```
I recieved this very weird email that only contained a file called "openme", it looks like an executable.

Can you see if there is anything weird in this file?

Credit

Developed by TomB(https://github.com/Tomaszbrauntsch)
```
Provided files:
- openme

### Solution

Since we are provided an executable, the best practice is to start out by running a `strings`
command on it. The challenge title also gives us a clue that this is the path to the solution.

I use [radare2's](https://rada.re/n/) strings `rabin2` tool instead of the basic `strings` command because it gives a more readable output. 

```bash
$ rabin2 -z openme
[Strings]
nth paddr      vaddr      len size section type  string
―――――――――――――――――――――――――――――――――――――――――――――――――――――――
0   0x00003008 0x00003008 20  21   .rodata ascii NICC{leaky_data_huh}
1   0x0000301d 0x0000301d 23  24   .rodata ascii Please enter the text:
2   0x00003035 0x00003035 10  11   .rodata ascii givemeflag
3   0x00003040 0x00003040 14  15   .rodata ascii Correct Flag!\n
4   0x00003050 0x00003050 49  50   .rodata ascii basic_string: construction from null is not valid
```

The flag is output as the first string.


Flag = `NICC{leaky_data_huh}`
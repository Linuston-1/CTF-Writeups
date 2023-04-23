## Challenge Title (200 Points)


### Problem
```
My friend sent me a bunch of pictures of deer and said there's a secret code in them or something. 
Can you figure out what he's talking about? 
He mentioned something about going from left to right in order and that there's only two types of a thing in all the pictures. 
He also said that it's not zeroes and ones, but wouldn't tell me what other two things it would be if not zero and one.

The flag will be in the format DawgCTF{THEFLAG}, alphabetical only, all capitals for the contents inside DawgCTF{}.
```

### Solution
We are given a total of 25 separate pictures of deer

However, there are only 5 unique pictures
These can be identified by their file sizes

1. 905 KB
2. 175 KB
3. 28 KB
4. 461 KB
5. 132 KB


In each of these pictures there are at least two deer

They are either male or female as identified by the presence of antlers

The encoding of the message is based on the order of male and female deer as read right-to-left

1. 905 KB - FM
2. 175 KB - MF
3. 28 KB - MM
4. 461 KB - FF
5. 132 KB - FMF


The complete ciphertext can be assmebled by putting all of the pictures' antler encoding into one string

1. 905 KB - FM
2. 175 KB - MF
3. 175 KB - MF
4. 28 KB - MM
5. 175 KB - MF
6. 175 KB - MF
7. 461 KB - FF
8. 175 KB - MF
9. 132 KB - FMF
10. 461 KB - FF
11. 175 KB - MF
12. 461 KB - FF
13. 905 KB - FM
14. 175 KB - MF
15. 175 KB - MF
16. 461 KB - FF
17. 28 KB - MM
18. 461 KB - FF
19. 175 KB - MF
20. 461 KB - FF
21. 905 KB - FM
22. 461 KB - FF
23. 175 KB - MF
24. 461 KB - FF
25. 175 KB - MF

The full string is `FMMFMFMMMFMFFFMFFMFFFMFFFFMMFMFFFMMFFMFFFFMFFMFFFMF`


I then used the [Cipher Identifier](https://www.dcode.fr/cipher-identifier) on Dcode.fr to figure out that the bacon cipher was being used

Putting the string into [Dcode's Bacon Cipher Decoder](https://www.dcode.fr/bacon-cipher) revealed the flag


Flag = `DawgCTF{NOREINDEER}`
## Bravo Six, Going Dark (200 Points)


### Problem
```
My friend is out on some weird work trip, and he sent me this video. 
Is he trying to say something?
He also attached what looks like a standard alphabet to the video, but in all capitals.
The flag format will be DawgCTF{ABCDEF} 
```

### Solution
We are given a video where a scrap of paper is shown with a message in a strange alphabet

Thanks to another CTF I participated in, I recognized it immediately as a Gravity Falls cipher

It is recognizable by the distinct 'I' with two dots on either side of it

After taking a screenshot of the note and importing it into Paint, I went to [Dcode.fr's Gravity Falls decoder](https://www.dcode.fr/gravity-falls-ciphers)

It turns out that there are 3 different ciphers: the Bill Cipher Cipher, The Author Cipher, and the Journal 3 Cipher
All of which share several characters


After looking through each of the pages, I landed on the [Bill Cipher Cipher](https://www.dcode.fr/gravity-falls-bill-cipher) as the correct one

It was the only cipher that had a glyph of two triangles on top of each other

From there it was just a matter of putting in the symbols and wrapping it in `DawgCTF{}` to get the flag


Flag = `DawgCTF{HEISWATCHINGYOU}`

◬
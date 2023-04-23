## Challenge Title (350 Points)


### Problem
```
My friend sent me another video. 
I'm kinda worried after the first one... 
There's also a file attached that contains only an uppercase alphabet, i.e A to Z. 
What's going on?! (Flag format A-Z same as first Bravo Six)
```

### Solution
This video features a flashing light that turns of an on at long and short intervals - a clue that we are dealing with morse code

I went through the video and wrote down the flashes separating letters based on long pauses

`... -.-. .--. .... .- ... -... .-. . .-`

I then put this into [CyberChef's from morse code tool](https://gchq.github.io/CyberChef/#recipe=From_Morse_Code('Space','Line%20feed')&input=Li4uIC0uLS4gLi0tLiAuLi4uIC4tIC4uLiAtLi4uIC4tLiAuIC4tCg)

The resulted in the string `SCPHASBREA`

It looks like it's still encrypted, but no cipher identifying tool picks anything up

Might as well try wrapping it in the flag format and see if it is correct


And guess what, it is!


Flag = `DawgCTF{SCPHASBREA}`
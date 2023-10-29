## Just Go Live


### Problem
```
Can you seem to find our flag on our service where we stream?

Be careful, things aren't as they seem!

Credit

Developed by theamazins17(https://github.com/theamazins17)
```

### Solution

The "service where we stream" is very likely [Twitch](https://www.twitch.tv/rtgame). In fact, there is a link to a Twitch channel on the home page of SpookyCTF. [NICCatNJIT](https://www.twitch.tv/niccatnjit) 

The stream title has several commands in it: !flag, !crazy, and !complain. None of them have very useful outputs though,

!flag
```
Nightbot: Sorry, but this is the wrong way to find the flag. Can you think of another way to find it?
```

!crazy
```
Nightbot: Crazy? I was crazy once. They locked me in a room. A rubber room! A rubber room with rats and rats made me crazy.
```

!complain
```
Nightbot: Please bring your complaints to our complaints bureau on our Discord. Or if you have questions open a ticket!
```


I decided to take a break from the challenge and leave it open in case someone else solved the challenge and Nightbot printed the flag in public chat. 

This worked, either because the solution was to wait or because someone else actually solved the challenge and the flag was shown to the public. 



Flag = `NICC{patience_my_purple_friend}`
## Capybara


### Problem
```
What a cute picture of a capybara!

Flag format: PCTF{}

Author: @txnner
```
File provided:
- capybara.jpeg
### Solution

To being with, I ran some simple commands on the provided image. However, nothing definitive turned up. 


```bash
$ file capybara.jpeg
capybara.jpeg: JPEG image data, JFIF standard 1.01, resolution (DPI), density 96x96, segment length 16, comment: "CREATOR: gd-jpeg v1.0 (using IJG JPEG v80), quality = 82", baseline, precision 8, 1200x630, components 3
```

```bash
$ strings capybara.jpeg

... Output omitted ...

x       <o
x       <o
G>4^
.l8g
Eua0
x       <o
G>4^
$}n$
x       <o
.]#W?
audio.wavPK
```

I did get a lead though, .jpeg files shouldn't have a string **"audio.wavPK"** in them. 

I decided to try and look for embedded files inside of the image that I could extract. A common tool for this is [Cyberchef](https://gchq.github.io/CyberChef/), but I used [7zip](https://www.7-zip.org/).


I was able to extract an audio file named **audio.wav** from the image.

After listening to this file I realized that it was morse code. 

Instead of trying to manually decode over a minute of morse code, I used [MorseCode.World](https://morsecode.world/international/decoder/audio-decoder-adaptive.html) to decode it for me.


The audio file decoded to the string: **"504354467B64305F7930555F6B4E30575F6830575F74305F523334445F6D307235335F433064333F7D"**

While this looks like random characters at first, on closer inspection it appears to be hexadecimal. And putting into a hex decoder gives us the flag.



Flag = `PCTF{d0_y0U_kN0W_h0W_t0_R34D_m0r53_C0d3?}`


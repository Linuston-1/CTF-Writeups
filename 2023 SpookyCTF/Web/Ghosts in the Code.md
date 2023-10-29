## Ghosts in the Code


### Problem
```
Some student here spun up a site where people are submitting their stories about all of the spooky stuff on campus!

This site is clearly haunted... or, at the very least, cursed.

https://niccgetsspooky.xyz

Flag Format: NICC{w0rds_may_c0nta1n_nums_and_chars!?} - but there are no apostrophes, commas, for colons

Credit

Developed by Cyb0rgSw0rd(https://github.com/AlfredSimpson)
```

### Solution

After opening the website and giving it a cursory lookover, the flag was not in plain sight.

I began the hunt by inspecting the webpage. Just expanding out the HTML showed the final part of the flag in a comment:`r3_2_l00k!}`
```html
<!--the final piece of your puzzle: r3_2_l00k!}-->
```

There was nothing else obvious in the body of the webpage, so I looked at the head. There were links to 3 other pages on the website.
- `./js/scary.js`
- `./css/bootstraps.css`
- `./css/spookystyles.css`


viewing scary.js in the browser dev tools debugger showed 2 parts of the flag

The first one was obvious since it was at the top of the file in its own function `NICC{gh0sts`
```javascript
function boo(){
    // You found part one:)
    alert("BOO! ahh! You found part one... -> NICC{gh0sts");
}
```

The second one was harder to find since it was embedded in a poem that would be printed to console `cky_2_s33_b`
```javascript
function printSpookyArray() {
    const spookyItems = [
        "The website flickered_with_ghostly code.",
        "Eerie whispers echoed in the digital void.",
        "Spectral images materialized_on the screen.",
        "Phantom clicks and keystrokes haunted the interface.",
        "Cursed data corrupted the webpage.",
        "The cursor moved as if_guided by unseen hands.",
        "A chilling presence_lingered in the browser.",
        "Cryptic symbols appeared in the source code.",
        "Links led to mysterious_and forbidden pages.",
        "The website's soul seemed lost in the code.",
        "Images_warped_into disturbing forms.",
        "Browsers froze in fear of the haunted site.",
        "Ghostly animations danced across the screen.",
        "Passwords changed on their_own accord.",
        "The website's flags_shifted to NICC{, but this was not one of them.",
        "Users reported strange and eerie pop-ups.",
        "The server logs_were_filled with cryptic messages.",
        "The website's pages seemed to rewrite themselves.",
        "Haunted links led to unknown realms.",
        "The site's domain was cursed by a malevolent spirit.",
        "E-mails from the beyond flooded the inbox.",
        "The search bar summoned eldritch results.",
        "The blog posts were haunted by ghostwriters.",
        "A ghost in the machine wreaked havoc on the layout.",
        "The navigation menu led to a ghost town.",
        "In the dark corners of the code, spirits whispered.",
        "The site's database contained lost souls of data.",
        "A cursed API returned spectral data.",
        "The login screen was guarded by a spectral guardian.",
        "Ectoplasmic glitches infected the JavaScript.",
        "Cursed forms submitted data to the netherworld.",
        "The site's SSL certificate was haunted by expired ghosts.",
        "404 pages displayed the faces of restless spirits.",
        "The homepage was an eerie portal to the unknown.",
        "Ghostly pixels haunted the image gallery.",
        "They shouted that you found the third!: cky_2_s33_b",
        "The site's footer contained cryptic incantations.",
        "The blog comments were filled with ghostly praise.",
        "Users reported being followed by digital apparitions.",
        "The website's sitemap led to a spectral maze.",
        "The site's analytics were haunted by phantom visitors.",
        "The FAQ section answered questions from beyond.",
        "E-mails sent from the site vanished into the abyss.",
        "Cursed cookies possessed the user's browser.",
        "The terms and conditions were written in ghostly ink.",
        "The site's contact form summoned spectral inquiries.",
        "The homepage's hero image was a cursed portrait.",
        "Pop-up notifications delivered cryptic prophecies.",
        "The loading spinner was possessed by impatience.",
        "A ghostly chatbot offered spectral customer support.",
        "The site's error messages spoke in riddles.",
        "The CAPTCHA was a test of one's psychic abilities.",
        "The site's forums were haunted by restless souls.",
        "User accounts were plagued by poltergeist passwords.",
        "The website's source code contained a haunted comment.",
        "The footer contained a link to the spirit world.",
        "The login screen asked for a secret from the afterlife.",
        "The privacy policy warned of spectral data collection.",
        "Ghostly images appeared in the image carousel.",
        "Cursed CSS styles warped the site's appearance.",
        "The site's AI chatbot conversed with ghostly wisdom.",
        "Ghostly SEO techniques boosted the site's ranking.",
        "The newsletter sign-up summoned spectral subscribers.",
        "The site's cookies were possessed by hungry spirits.",
        "A cursed pop-up window asked for your soul.",
        "The website's dark theme was haunted by shadows.",
    ];

    for (let i = 0; i < spookyItems.length; i++) {
        console.log(spookyItems[i]);
    }
}
```


Moving onto the CSS files, there is nothing of note in spookystyles.css, However bootstraps.css does have a piece of the flag `_c@n_b3_tr1`
```css
.flg-txt-pt2{
	value: '_c@n_b3_tr1';
}
```


Now that all of the main webpage files have been exhausted, I went to look at other tabs of the browser dev tools menu. Specifically the storage and network tabs.

The storage tab lets you look at website cookies among other data stored between sessions. 

There are several cookies on this website that have the name flagpart5 and the value `0u_kn0w_wh3`


The network tab lets you see which files the website is loading on your computer.  

Only one file could not be loaded and it was located at https://niccgetsspooky.xyz/4thPartofyourflag/'u7_n0t_1f_y. Which shows us 4th part of the flag is `0u_kn0w_wh3`


Now that we have all parts of the flag, we just need to assemble them to complete the challenge
- `NICC{gh0sts`
- `_c@n_b3_tr1`
- `cky_2_s33_b`
- `u7_n0t_1f_y`
- `0u_kn0w_wh3`
- `r3_2_l00k!}`


Flag = `NICC{gh0sts_c@n_b3_tr1cky_2_s33_bu7_n0t_1f_y0u_kn0w_wh3r3_2_l00k!}`
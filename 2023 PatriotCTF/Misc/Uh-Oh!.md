## Uh-Oh!


### Problem
```
Beginner

Uh Oh! While trying to add passwords to my wordlist, I accidentally added my own phone number! Can you tell me what line it's on?

https://en.wikipedia.org/wiki/North_American_Numbering_Plan#Modern_plan

Make sure the phone number follows this format: (NPA) XXX-XXXX

For example (123) 456-7890

Flag format: PCTF{linenumber_phonenumonlynumbers}

Author: @angr404
```
Provided Files:
- rockyou.txt
### Solution

On seeing that the provided password list was rockyou.txt, I thought of 2 different options:

1. Compare the provided rockyou.txt to an unmodified version.
2. Search the modified rockyou.txt for anything that matches the format we are given. 

Option 1 would be a good option if we did not know the format of the text we are looking for, but since we do, option 2 is the way to go.


When searching for a string that matches certain characteristics, regex is the way to go.

There are many websites that can help you generate an expression so you don't have to figure it out by hand. I used [Regex-generator.olafneumann.org](https://regex-generator.olafneumann.org/?sampleText=(111)%20111-1111&flags=i&selection=0%7CParentheses,1%7CNumber,5%7CCharacter,6%7CNumber,9%7CCharacter,10%7CNumber)

I ended up with the expression: **\\(\[0-9]+\) \[0-9]+-\[0-9]+**


The final step is to load up the modified rockyou.txt into a text editor that supports regex. 

For this I used [VSCode](https://code.visualstudio.com/)


I got one match one line **7731484** for **(404) 303-7283**



Flag = `PCTF{7731484_4043037283}`

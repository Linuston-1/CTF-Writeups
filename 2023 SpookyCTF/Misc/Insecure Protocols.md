## Insecure Protocols 


### Problem
```
I just spun up my first website with a login page and everything! My friend tells me my page isn't secure and I'm not sure why.

Credit

Developed by BonsaiUmai(https://github.com/JustinTecson)
```
Provided files:
- insecure.pcap
### Solution

[Wireshark](https://www.wireshark.org/) is the best tool to use for analyzing packet capture files. One of the most useful features of Wireshark is the ability to search through packet bytes.

This lets us search for a specific string in all of the packets of insecure.pcap

Searching the packet bytes can be done by pressing ctrl+f and switching the default setting "Packet list" to "Packet bytes"

By searching for the first 4 letters of the flag format "NICC" we are immediatley brought to the packet with the flag. 

```
Form item: "uname" = "NICC{h77p_15_1n53cur3}"
Form item: "pass" = "password"
```

The username and password are in plaintext letting us easily get the flag.

Flag = `NICC{h77p_15_1n53cur3}`
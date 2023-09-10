## WPA


### Problem
```
I really need to get on my friends WiFi, but he won't give me the password. I think he think's I'll mess around on his network. I started a packet capture and left it running a while, I think someone connected to the network before I stopped the capture. Can you help me?

Flag format: PCTF{password}

Author: @elbee#3779
```
Files provided:
- savedcap.cap
### Solution

The best tool for cracking a Wi-Fi password when given a packet capture is  [Aircrack-ng](https://www.aircrack-ng.org/).

All you have to do is give it a packet capture file and a wordlist. I tend to start with the rockyou.txt wordlist.

```
$ aircrack-ng savedcap.cap -w /usr/share/wordlists/rockyou.txt
Reading packets, please wait...
Opening savedcap.cap
Read 888 packets.

   #  BSSID              ESSID                     Encryption

   1  52:E2:4D:0A:A6:36  Pctf wifi challenge       WPA (1 handshake)

Choosing first network as target.

Reading packets, please wait...
Opening savedcap.cap
Read 888 packets.

1 potential targets

                               Aircrack-ng 1.7

      [00:00:04] 2107/14344392 keys tested (571.58 k/s)

      Time left: 6 hours, 58 minutes, 12 seconds                 0.01%

                           KEY FOUND! [ qazwsxedc ]


      Master Key     : D9 2A 24 C3 1D DB EF C0 58 AF 10 9F F2 F5 DE E9
                       0C B6 EC F9 59 4E 39 7C 6E 50 E8 B5 3D 61 7E C4

      Transient Key  : A8 6F FF 4C D2 0A 0B 59 5B 17 6E 27 32 63 29 9C
                       D3 A6 4D 25 80 02 DF B8 39 C7 F1 46 08 E5 88 24
                       2F 50 8A 5E D9 65 17 AD C6 AC DC 83 00 D6 D3 39
                       37 77 DF 14 83 00 FF 3D E1 6D 13 CA D3 B4 40 C9

      EAPOL HMAC     : 2F F5 73 C8 A5 66 B0 60 7D EF 8F 51 B0 64 F6 65


```

The password was found to be **qazwsxedc**.

All that is left to be done is wrap the password in PCTF{} and submit it

Flag = `PCTF{qazwsxedc}`
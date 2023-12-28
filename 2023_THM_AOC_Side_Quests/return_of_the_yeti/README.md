# The Return of the Yeti (THM Advent of Cyber '23 Side Quest 1 Difficulty: Hard)

## Introduction

Using the QR code you pieced together in Advent of Cyber Side Quest Main you are given the url for the the first side quest. 
 .

<p align="left">
  <img height=700 img src=./readme_assets/qr-code-1.png/>
</p>

Scan the QR code and you are in! Welcome to [Return of the Yeti](https://tryhackme.com/room/adv3nt0fdbopsjcap)!

<p align="left">
  <img height=500 img src=./readme_assets/challenge.PNG/>
</p>

<p align="left">
  <img height=500 img src=./readme_assets/hints.PNG/>
</p>


You are give a file `VanSpy.pcapng` and 5 questions to answer.

*Question 1 - What's the name of the WiFi network in the PCAP?*
*Question 2 - What's the password to access the WiFi network?*
*Question 3 - What suspicious tool is used by the attacker to extract a juicy file from the server?*
*Question 4 - What is the case number assigned by the CyberPolice to the issues reported by McSkidy?*
*Question 5 - What is the content of the `yetikey1.txt` file?*

## Solution

Open the .pcapng file in Wireshark to begin. You should immediately see the answer to Q1 in the Beacon packets.

<p align="left">
  <img height=300 img src=./readme_assets/wifi-network.PNG/>
</p>

To find the answer to Q2, the wifi password, we need to find the right tool to use. After a little googling I found that `aircrack-ng` was the best tool for this.

To use `aircrack-ng` we will need the wifi name and the source MAC address from the pcapng file. 

Aircrack-ng does not work with pcapng files and will need to be converted to a .pcap file first. Use tshark in your terminal to get this accomplished.

`tshark -F pcap -r VanSpy.pcapng -w VanSpy.pcap`

Now use the information you gathered to run `aircrack-ng` to get the password.

`aircrack-ng -w /usr/share/wordlists/rockyou.txt -b 22:c7:12:c7:e2:35 VanSpy.pcap`

<p align="left">
  <img height=300 img src=./readme_assets/aircrack-ng.PNG/>
</p>

Now that we have the wifi network name and password we can add it to the IEEE 802.11 protocol preferences. Use the information from [wireshark.org]*(https://wiki.wireshark.org/HowToDecrypt802.11) for more information.

<p align="left">
  <img height=300 img src=./readme_assets/decryption.PNG/>
</p>

*edit/ preferences/ protocols/ IEEE 802.11/ click edit/ add wps-pwd*

You should now see more packets. Follow the TCP stream to the end to see the suspicious tool used.

<p align="left">
  <img height=300 img src=./readme_assets/mimikatz2.PNG/>
</p>

You will find some really interesting information in the TLS stream. The hacker used RDP to remote into the INTERN-PC and download the Security Certificate.

Notice the public and private export of the certificate.

<p align="left">
  <img height=300 img src=./readme_assets/export.PNG/>
</p>

The hacker then opened the .pfx file which allows us to see the base64 string we need to recreate the certificate.

<p align="left">
  <img height=300 img src=./readme_assets/base64.PNG/>
</p>

The .pfx file is password protected. Using google you find the default password that Mimikatz uses is mimikatz.

First we have to convert the base64 string to binary  
`enc -base64 -A -d -in base64.pfx -out converted.pfx`

Next you convert the `.pfx` file to .pem using `openssl` You will be prompted several times for a password. I used mimikatz each time to avoid confusion.
`openssl pkcs12 -in converted.pfx -out file.nokey.pem -nokeys`
`openssl pkcs12 -in converted.pfx -out file.withkey.pem`
`openssl rsa -in file.withkey.pem -out file.key`
`cat file.nokey.pem file.key > file.combo.pem`

We now need to add the the new `.pem` file to the TLS decrypt preferences as well as the RSA decrypt preferences.

*edit/ preferences/ protocols/ TLS/ click edit/*

<p align="left">
  <img height=300 img src=./readme_assets/tls.PNG/>
</p>

<p align="left">
  <img height=300 img src=./readme_assets/rsa.PNG/>
</p>

This should decrypt the TLS and RDP packets and we should be ready to search for answers to Q4 and Q5.

Going back to the TLS stream will give you everything you need.

<p align="left">
  <img height=300 img src=./readme_assets/tls-capture1.PNG/>
</p>

Case number is in packet 17870 - in the decrypted TLS tab

<p align="left">
  <img height=300 img src=./readme_assets/packet.PNG/>
</p>


In packet `34383` you find `y.e.t.i.k.e.y.1...t.x.t`. Now we have to find the contents of the file.

<p align="left">
  <img height=300 img src=./readme_assets/tls-capture2.PNG/>
</p>

In packet `35686` we find a string of hex

<p align="left">
  <img height=300 img src=./readme_assets/yetitext.png/>
</p>

This is our answer for Q5.








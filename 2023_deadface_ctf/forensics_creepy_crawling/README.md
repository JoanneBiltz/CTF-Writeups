# Creepy Crawling (forensics)

## Introduction

<p align="left">
  <img height=700 img src=./readme_assets/creepy-challenge.PNG/>
</p>

> One of our clients, TGRI, had an SSH server compromised at one of their smaller remote locations. Their only security analyst was fired and “accidentally” deleted information specific to the attack. Thankfully, TGRI still has the PCAP that captured the SSH brute force attack. What SSH protocol did TGRI run that was eventually compromised by DEADFACE?

> Submit the SSH protocol as the flag: flag{SSH-1.1.1: Simple SSH Server}

You are given a pcap file

## Solution

I just searched for SSH as a string and looked at the packets until I found the right one.

<p align="left">
  <img height=300 img src=./readme_assets/creepy-flag.PNG/>
</p>

## Flag

**`flag{SSH-2.0-9.29 FlowSsh: Bitvise SSH Server (WinSSHD) 9.29}`**

## Tools






# You've Been Ramsomwared (stego)

## Introduction

<p align="left">
  <img height=700 img src=./readme_assets/ransom-challenge.PNG/>
</p>

> DEADFACE is taunting GlitterCo with their latest ransomware attack. According to our intel, the attackers like to leave a calling card in their attacks. If we can figure out which DEADFACE actor executed this attack, we might be able to figure out a way around paying. Can you find anything in this screenshot that might point to which attacker ran this ransomware attack?

You are given a png file.

<p align="left">
  <img height=700 img src=./readme_assets/ransomwared.png/>
</p>

## Solution

Did all of the usual stego tools and found nothing interesting. 
Loaded the file into [Aperi Solve](https://www.aperisolve.fr/) and found a bunch of binary numbers at the bottom of the photo.

<p align="left">
  <img height=700 img src=./readme_assets/image_g_6.png/>
</p>

```
01010100 01101000 01101001 01110011 00100000 01110010 01100001 01101110 01110011 01101111 01101101 01110111 01100001 01110010 01100101 00100000 01100010 01110010 01101111 01110101 01100111 01101000 01110100 00100000 01110100 01101111 00100000 01111001 01101111 01110101 00100000 01100010 01111001 00100000 01101101 01101001 01110010 01110110 01100101 01100001 01101100 00101110
```

Converts to `This ransomware brought to you by mirveal`.

## Flag

**`flag{mirveal}`**

## Tools

- [Aperi Solve](https://www.aperisolve.fr/)





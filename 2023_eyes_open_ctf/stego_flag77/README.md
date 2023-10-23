# flag77, (Stego, 69 solves, 25p)

## Introduction

<p align="left">
  <img height=500 img src=./readme_assets/flag77-challenge.PNG/>
</p>

You are given a jpg file.

<p align="left">
  <img height=400 img src=./readme_assets/steg1.jpg/>
</p>

## Solution

I did the usual stego tricks (`file, exiftool, strings, binwalk`) with no success. I installed `stegseek` and gave it a try using `stegseek steg1.jpg rockyou.txt` and found the flag.

<p align="left">
  <img height=300 img src=./readme_assets/flag77-stegseek.PNG/>
</p>

## Flag

**`flag{74f11red}`**

## Tools

- [stegseek](https://github.com/RickdeJager/stegseek)


# flag79, (Stego, 69 solves, 50p)

## Introduction

<p align="left">
  <img height=500 img src=./readme_assets/flag79-challenge.PNG/>
</p>

You are given a png file.

## Solution

The image is a white square. I did the usual stego tricks (`file, exiftool, strings, binwalk`) with no success. I opened the image using `StegOnline` and found a QR code.

<p align="left">
  <img height=600 img src=./readme_assets/79-qr.PNG/>
</p>

When you go to the link the flag page appears only for a second then you get spam pages. I contacted the CTF to see if something was wrong with the challenge but they said it was a part of it. I was finally able to get out of the spam pages and see the flag.

## Flag

**`flag{aqp4mpf2}`**

## Tools

- [StegOnline](https://stegonline.georgeom.net/upload)


# Fetching Secrets (stego)

## Introduction

<p align="left">
  <img height=700 img src=./readme_assets/fetching-challenge.PNG/>
</p>

> This image was found on Ghost Town. Looks like one of DEADFACE’s newest members is new to steganography. See if you can find any hidden information in this image. Knowing information about the image may help to reveal the flag.

You are given a .jpg file.

<p align="left">
  <img height=700 img src=./readme_assets/cyberdog.jpg/>
</p>

## Solution

I tried all of the usual stego tools but haven't found anything.

Did a little googling and ran across [stegseek](https://github.com/RickdeJager/stegseek).
`stegseek cyberdog.jpg /usr/share/wordlists/rockyou.txt`

The password is `kira`

<p align="left">
  <img height=700 img src=./readme_assets/fetching-flag.PNG/>
</p>

## Flag

**`flag{g00d_dawg_woofw00f}`**

## Tools

- [stegseek](https://github.com/RickdeJager/stegseek)




# Unsupported Format 1, (forensics)

## Introduction

> My friend sent me a picture of his brand new computer, but something strange happened to it and now it says "Unsupported Format" when I try to open it. Can you try to help me recover the image?

## Solution

The jpeg file does not open. 

Use a hex editor (I use [HxD](https://mh-nexus.de/en/hxd/) to open the file. 

You can see an area that says CORRUPTED over and over. Remove everything with CORRUPTED and save the file.

You are now able to open the image and get the flag.

<p align="left">
  <img height=500 img src=./readme_assets/Flag2.jfif/>
</p>

## Flag

**`PCTF{c0rrupt3d_b1t5_4r3_c00l}`**

## Tools

- [HxD](https://mh-nexus.de/en/hxd/)


# Electric Steel (stego)

## Introduction

<p align="left">
  <img height=700 img src=./readme_assets/steel-challenge.PNG/>
</p>

> Check out this image DEADFACE left on one of their victims' machines. We tried a couple tools and they didn’t reveal anything. Take a look and see what you can find.

You are given a .png file.

<p align="left">
  <img height=700 img src=./readme_assets/electric-steel.png/>
</p>

## Solution

Use `binwalk -e` to extract files. Unzip the tar file to get the flag.

```
binwalk electric-steel.png

# DECIMAL       HEXADECIMAL     DESCRIPTION
# --------------------------------------------------------------------------------
# 0             0x0             PNG image, 1232 x 928, 8-bit/color RGB, non-interlaced
# 2767          0xACF           Zlib compressed data, default compression
# 1435378       0x15E6F2        TIFF image data, big-endian, offset of first image directory: 8
# 1435914       0x15E90A        Copyright string: "Copyright (c) 1998 Hewlett-Packard Company"
# 1467642       0x1664FA        gzip compressed data, from Unix, last modified: 2023-06-04 01:14:27
```

## Flag

**`flag{3L3ctr1c_5t33L_b1G_H41R}`**

## Tools

- **`binwalk`**




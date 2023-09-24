# A Petty Wage in Regret (stenography, 94 solves, 200p)

## Introduction

<p align="left">
  <img height=500 img src=./readme_assets/challenge.png/>
</p>

Here is the .jpg file.

<p align="left">
  <img height=500 img src=./readme_assets/DF2.jpg/>
</p>

## Task analysis

The jpg file has obvious distortion which usually means there is another file hidden inside.

## Enumeration

**`exiftool`** gives us a user comment: **`3A3A50312F323A3A20706F6374667B757773705F3768335F7730726C645F683464`**

Convert from hex and you get **`::P1/2:: poctf{uwsp_7h3_w0rld_h4d`**
This tells us there are two parts to the flag and this is part 1. 

Using **`stegsolve`** you can see numbers under the original picture but they are very fuzzy and hard to see.

<p align="left">
  <img height=500 img src=./readme_assets/ds2fuzzy.png/>
</p>

Using **`Forensically`** we can get a better view of the text using the Error Detection option.

<p align="left">
  <img height=500 img src=./readme_assets/DS2.png/>
</p>

The letters are hard to read so I tried extracting a second image from the first. I tried carving out the jpeg inside the jpeg but it was just a thumbnail image of the original and not useful.

The picture above is obviously part 2 of the flag but was unable to read the the letter/number before 1257 **`poctf{uwsp_7h3_w0rld_h4d_17_?1275}`**

## Solution

Through trial and error I finally got the flag.

## Tools

**`stegsolve`**

https://stegonline.georgeom.net/

https://29a.ch/photo-forensics/#forensic-magnifier

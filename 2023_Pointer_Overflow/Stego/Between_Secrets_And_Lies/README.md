# Between Secrets and Lies (stenography, 12 solves, 300p)

## Introduction

<p align="left">
  <img height=700 img src=./readme_assets/challenge.PNG/>
</p>

Here is the .png image.

<p align="left">
  <img height=500 img src=./readme_assets/bean.png/>
</p>

## Task analysis

There are obvious colored pixels in the bottom right corner.

<p align="left">
  <img height=300 img src=./readme_assets/colors.PNG/>
</p>

## Enumeration

**`exiftool`** shows the image is 2.2 MG which is large for a CTF image.
**`strings`** doesn't show anything interesting.
**`foremost`** and **`binwalk`** extract a duplicate of the original image. This can be done over and over with the same result.
**`zsteg`** doesn't show anything useful.
**`stegsolve`** gave me nothing.

I opened the image in gimp and extracted the hex codes for the color blocks = ffff6642ffff51da4cff6e3c3c46ff
Decoding in https://www.rapidtables.com/convert/number/ascii-hex-bin-dec-converter.html gives me nothing.
Tried submitting poctf{uwsp_ffff6642ffff51da4cff6e3c3c46ff} but no go.


## Solution

Used stegonline to extract the LSB. It took a lot of trial and error but finally got the flag.

<p align="left">
  <img height=500 img src=./readme_assets/beans_solve.PNG/>
</p>

## Tools

https://stegonline.georgeom.net/checklist



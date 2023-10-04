# Congratulations, (forensics)

## Introduction

> Congratulations on making it this far, here's an email attachment.

## Solution

The downloaded file is a Word document.

Use **`olevba --reveal Congratulations.docm`** which helps extract any macros in the Word document.

<p align="left">
  <img height=900 img src=./readme_assets/macro.PNG/>
</p>

This section looked promising: **`[char]0x50 + [char]0x43 + [char]0x54 + [char]0x46 + [char]0x7B + [char]0x33 + [char]0x6E + [char]0x34 + [char]0x62 + [char]0x6C + [char]0x33 + [char]0x5F + [char]0x6D + [char]0x34 + [char]0x63 + [char]0x72 + [char]0x30 + [char]0x35 + [char]0x5F + [char]0x70 + [char]0x6C + [char]0x7A + [char]0x5F + [char]0x32 + [char]0x37 + [char]0x33 + [char]0x31 + [char]0x35 + [char]0x36 + [char]0x37 + [char]0x30 + [char]0x7D`**

Reformat so we can decode **`50 43 54 46 7B 33 6E 34 62 6C 33 5F 6D 34 63 72 30 35 5F 70 6C 7A 5F 32 37 33 31 35 36 37 30 7D`**

Use [RapidTables](https://www.rapidtables.com/convert/number/ascii-hex-bin-dec-converter.html) to convert the hex for the flag. 

## Flag

**`PCTF{3n4bl3_m4cr05_plz_27315670}`**

## Tools

- **`olevba`**
- [RapidTables](https://www.rapidtables.com/convert/number/ascii-hex-bin-dec-converter.html)


# Chicken Wings (warmup, 1247 solves, 50 points)

## Introduction

<p align="left">
  <img height=400 img src=./readme_assets/chicken-challenge.PNG/>
</p>

## Solution

The file does not have an extension. Opening it up in notepad looks interesting.

<p align="left">
  <img height=200 img src=./readme_assets/icons.PNG/>
</p>

Using `file` on the file says we have `Unicode text, UTF-8 text`, with no line terminators.

Online decoders don't seem to like this code. I tried converting to binary then to ascii with no success. 

The description hints at wingdings font. Found a wingdings online converter https://lingojam.com/WingdingsTranslator and got the flag.

## Flag

**`flag{e0791ce68f718188c0378b1c0a3bdc9e}`**

## Tools

- `file`
- [wingdings Translator](https://lingojam.com/WingdingsTranslator)




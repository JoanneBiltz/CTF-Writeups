# BaseFFFF+1 (warmup, 1266 solves, 50 points)

## Introduction

<p align="left">
  <img height=400 img src=./readme_assets/base-challenge.PNG/>
</p>

## Solution

The file is a text file with `鹎驣𔔠𓁯噫谠啥鹭鵧啴陨驶𒄠陬驹啤鹷鵴𓈠𒁯ꔠ𐙡啹院驳啳驨驲挮售𖠰筆筆鸠啳樶栵愵欠樵樳昫鸠啳樶栵嘶谠ꍥ啬𐙡𔕹𖥡唬驨驲鸠啳𒁹𓁵鬠陬潧㸍㸍ꍦ鱡汻欱靡驣洸鬰渰汢饣汣根騸饤杦样椶𠌸`.

I tried `Google Translate` and it has a few words of Chinese but not the whole thing.


<p align="left">
  <img height=300 img src=./readme_assets/translate.PNG/>
</p>

Ran the ciphertext through `cyberchef` and `dcode` but got nothing. I thought the base64 hint would lead to another base code but none worked.

I was overthinking this. The title is `baseffff+1`. `ffff = 65535 + 1 = 65536`. Convert from `base65536` using [Better Converter](https://www.better-converter.com/Encoders-Decoders/Base65536-Decode) to get the flag.

<p align="left">
  <img height=400 img src=./readme_assets/base-flag.PNG/>
</p>

## Flag

**`flag{716abce880f09b7cdc7938eddf273648}`**

## Tools

- `base65536`
- [Better Converter](https://www.better-converter.com/Encoders-Decoders/Base65536-Decode`)




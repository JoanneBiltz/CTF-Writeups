# Capybara, (forensics)

## Introduction

> What a cute picture of a capybara!

<p align="left">
  <img height=700 img src=./readme_assets/capybara.PNG/>
</p>

## Solution

**`strings`** gives us the text **`audio.wavPK`** so we know we are looking for an audio file hidden in the image.

Use **`binwalk -e`** to extract the **`audio.wav`** file.

Listening to the audio it sounds like **`morse code`**. Use [MorseCode.World](https://morsecode.world/international/decoder/audio-decoder-adaptive.html) to extract the message from the audio recording.

**`50 43 54 46 7B 64 30 5F 79 30 55 5F 6B 4E 30 57 5F 68 30 57 5F 74 30 5F 52 33 34 44 5F 6D 30 72 35 33 5F 43 30 64 33 3F 7D`**

Use [RapidTables](https://www.rapidtables.com/convert/number/ascii-hex-bin-dec-converter.html) to decode the hex for the flag.

## Flag

**`PCTF{d0_y0U_kN0W_h0W_t0_R34D_m0r53_C0d3?}`**

## Tools

- **`strings`**
- **`binwalk`**
- [MorseCode.World](https://morsecode.world/international/decoder/audio-decoder-adaptive.html)
- [RapidTables](https://www.rapidtables.com/convert/number/ascii-hex-bin-dec-converter.html)


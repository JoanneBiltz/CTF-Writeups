# Cereal Killer 01 (reverse engineering)

## Introduction

<p align="left">
  <img height=700 img src=./readme_assets/cereal1-challenge.PNG/>
</p>

> How well do you know your DEADFACE hackers? Test your trivia knowledge of our beloved friends at our favorite hactivist collective! We’ll start with bumpyhassan. Even though he grates on TheZeal0t a bit, we find him to be absolutely ADORKABLE!!!

> Choose one of the binaries below to test your BH trivia knowledge.

> Enter the flag in the format: flag{Ch33ri0z_R_his_FAV}.

You are given a binary file.

## Solution

Run the binary to see what it does:

<p align="left">
  <img height=300 img src=./readme_assets/cereal1-run.PNG/>
</p>

Using `strings` on the binary we find an interesting string of text 
`I&_9a%mx_tRmE4D3DmYw_9fbo6rd_aFcRbE,D.D>Y[!]!'!q`

I tried using [CyberChef](https://gchq.github.io/CyberChef/) magic but got nothing. Looked at the code in [dogbolt](https://dogbolt.org/) and found that the flag is shifted. We can take the ciphertext we found and remove every other letter to get the flag.

## Flag

**`flag{I_am_REDDY_for_FREDDY!!!}`**

## Tools

- **`strings`**
- [CyberChef](https://gchq.github.io/CyberChef/)
- [dogbolt](https://dogbolt.org/)




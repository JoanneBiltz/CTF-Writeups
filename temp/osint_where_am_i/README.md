# Where am I? (OSINT, 1272 solves, 50 points)

## Introduction

<p align="left">
  <img height=400 img src=./readme_assets/whereami-challenge.PNG/>
</p>

## Solution

Use strings on the jpg and you find a base64 string in the image description. `ZmxhZ3tiMTFhM2YwZWY0YmMxNzBiYTk0MDljMDc3MzU1YmJhMik=`

Convert in [Cyberchef](https://gchq.github.io/CyberChef/) for the flag.

## Flag

**`flag{b11a3f0ef4bc170ba9409c077355bba2)`**

## Tools

- `strings`
- [Cyberchef](https://gchq.github.io/CyberChef/)

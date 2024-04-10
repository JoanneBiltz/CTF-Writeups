# Bad Memory (forensics, 255 solves, 50 points)

## Introduction

<p align="left">
  <img height=400 img src=./readme_assets/memory-challenge.PNG/>
</p>

## Solution

I know that I have to find a password and MD5 hash it for the flag. Using `file` it says the file is `Data`. Opening as txt is gibberish.

I've tried grepping for password, opening in autopsy, opening in FTK, but most programs can't determine the file structure. Also tried foremost to see if it would extract the deleted files.

Reinstalled `Volatiltiy3` in Kali and got it working. Worked my way through the windows.<commands> to see what will give me the password.

Used `python3 vol.py -f /media/sf_Kali_Shared/huntress/memory/image/image.bin  windows.hashdump.Hashdump` and received a few hashes to check out.

<p align="left">
  <img height=200 img src=./readme_assets/memory-hash.PNG/>
</p>

Cracked the nthash `ab395607d3779239b83eed9906b4fb92` using [CrackStation](https://crackstation.net/) and found `goldfish#`.

<p align="left">
  <img height=200 img src=./readme_assets/memory-crack.PNG/>
</p>

Used [md5hashgenerator](https://www.md5hashgenerator.com/) to generate an MD5 hash of `goldfish#` for the flag.

## Flag

**`flag{2eb53da441962150ae7d3840444dfdde}`**

## Tools

- `file`
- [Volatiltiy3](https://www.volatilityfoundation.org/)
- [CrackStation](https://crackstation.net/)
- [md5hashgenerator](https://www.md5hashgenerator.com/)

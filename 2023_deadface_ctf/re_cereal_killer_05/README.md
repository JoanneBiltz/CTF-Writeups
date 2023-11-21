# Cereal Killer 05 (reverse engineering)

## Introduction

<p align="left">
  <img height=700 img src=./readme_assets/cereal5-challenge.PNG/>
</p>

> We think Dr. Geschichter of Lytton Labs likes to use his favorite monster cereal as a password for ALL of his accounts! See if you can figure out what it is, and keep it handy! Choose one of the binaries to work with.

> Enter the answer as flag{WHATEVER-IT-IS}.

You are given a binary file.

## Solution

Run the binary to see what it does:

<p align="left">
  <img height=200 img src=./readme_assets/cereal5-run.PNG/>
</p>

Nothing in `strings`.

Looking at the binary in [dogbolt](https://dogbolt.org/) I found the password for the program.
`Xen0M0rphMell0wz`

Running the binary with the password gives us the flag.

<p align="left">
  <img height=200 img src=./readme_assets/cereal5-flag.PNG/>
</p>

## Flag

**`flag{XENO-DO-DO-DO-DO-DO-DOOOOO}`**

## Tools

- **`strings`**
- [dogbolt](https://dogbolt.org/)




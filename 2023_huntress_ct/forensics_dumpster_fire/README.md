# Dumpster Fire (forensics, 957 solves, 50 points)

## Introduction

<p align="left">
  <img height=400 img src=./readme_assets/dumpster-challenge.PNG/>
</p>

## Solution

The provided zip file contains an entire linux file system. Since we are looking for passwords I checked out `etc/shadow` and `ect/passwd`.  Normally shadow contains hashed passwords but this one has all of the hashes deleted.

<p align="left">
  <img height=500 img src=./readme_assets/dumpster-shadow.PNG/>
</p>

The description mentions foxes so looked in the firefox folder and grepped passw. It gave me `encryptedPassword":"MFIEEPgAAAAAAAAAAAAAAAAAAAEwFAYIKoZIhvcNAwcECEcjS+e6bXjFBCgCQ0p/1wCqPUmdgXdZWlohMXan4C3jD0bQgzsweyVEpAjJa+P9eOU4"` which I can't seem to decrypt. 

Using [Firefox Decrypt](https://github.com/unode/firefox_decrypt) we get the flag.

<p align="left">
  <img height=200 img src=./readme_assets/dumpster-flag.PNG/>
</p>

## Flag

**`flag{35446041dc161cf5c9c325a3d28af3e3}`**

## Tools

- `grep`
- [Firefox Decrypt](https://github.com/unode/firefox_decrypt)



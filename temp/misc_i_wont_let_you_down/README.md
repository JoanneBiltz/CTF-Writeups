# I Wont Let You Down (misc, 1414 solves, 50 points)

## Introduction

<p align="left">
  <img height=400 img src=./readme_assets/letyoudown-challenge.PNG/>
</p>

## Solution

Go to the linked website and it's a rick roll.

Use `nmap` on the ip address to get the open ports.

<p align="left">
  <img height=200 img src=./readme_assets/nmap.PNG/>
</p>

Tried to `ssh` into the site but got a warning that shh is off limits.

<p align="left">
  <img height=200 img src=./readme_assets/ssh.PNG/>
</p>

Used `netcat` to access the site `nc 155.138.162.158 8888`.

Get rick rolled again but with the flag at the end.

<p align="left">
  <img height=600 img src=./readme_assets/rick-flag.PNG/>
</p>

## Flag

**`flag{93671c2c3BeeB7250B770361ace37b02}`**

## Tools

- `nmap`
- `ssh`
- `netcat`

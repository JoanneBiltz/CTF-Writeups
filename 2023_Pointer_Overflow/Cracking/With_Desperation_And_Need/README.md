# With Desperation and Need (cracking, 16 solves, 300p)

## Introduction

<p align="left">
  <img height=500 img src=./readme_assets/challenge.PNG/>
</p>


## Task analysis

We need to figure out what the VeraCrypt file extension is and crack the password using the wordlist **`rockyou.txt`**.  

## Solution

The VeraCrypt file extension is **`.hs`** so we change the file to **`crack3.hs`**.

The hint in the description tells us **`The password is alphanumeric (A-Z, a-z, 0-9), contains no special characters, and the first three characters are gUn`**

Using the hint we grep the rockyou.txt file to **`crack.txt`** to use with hashcat. **`grep "^[A-Za-z0-9]"  rockyou.txt > crack.txt`**

<p align="left">
  <img height=500 img src=./readme_assets/gUn.PNG/>
</p>

We get lucky and only one password matches the hint given **`gUnGNmZg6E6x0k1RgrkS`**. No need to crack with hashcat.

Download a VeraCrypt container viewer to open the file. Input the password **`gUnGNmZg6E6x0k1RgrkS`**. Inside the container is a file named **`flag.txt`** which contains our flag.

## Tools

**`grep`**

https://www.veracrypt.fr/en/Home.html

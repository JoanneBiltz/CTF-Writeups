# We Mighty, We Meek (crack, 24 solves, 100 points)

## Introduction

<p align="left">
  <img height=700 img src=./readme_assets/mighty-challenge.PNG/>
</p>

## Task analysis

Crack the password for the excel file and find the flag.

## Enumeration

This was a tough challenge and very much a collaborative effort to solve.

We changed the extension to **`.xlsx`** and tried opening in Excel. It worked but the file is password protected. While researching Microsoft password protected files we found **`office2john.py`**. We used **`office2john.py`** to hash the excel file. **`crack1.xlsx:$office$201310000025616912a7246e4f68e941d6c46fc6e08a4832260c3a993eaaef1546b8089d588fbe8*94d51fe5b72f73d422fba69b6f32fa32e363aa5c94ba41b4f86e821a04a21774`**

We found the encryption metadata. Maybe this can help us crack the file:
```
<dataIntegrity 
encryptedHmacKey="LBSnKZqMetHKGQbb88XEq8rtKa8FiQJYzbA4///SvY3fa4oKRWGerkBW/lJYgUY5zQZE8sRVlKt4kKicd2jl9g==" 
encryptedHmacValue="qwvpbO7p4sBfZwIWOqhG02g0U+ju7+gewHaN2+gLpdkPb8GgZxG+VJr6X+8D651mWQmSi5q+Hleqfec2yt6z5A=="/>
<keyEncryptors>
<keyEncryptor 
uri="http://schemas.microsoft.com/office/2006/keyEncryptor/password">
<p:encryptedKey 
spinCount="100000" 
saltSize="16" 
blockSize="16" 
keyBits="256" 
hashSize="64" 
cipherAlgorithm="AES" 
cipherChaining="ChainingModeCBC" 
hashAlgorithm="SHA512" 
saltValue="kSpyRuT2jpQdbEb8bgikgw==" 
encryptedVerifierHashInput="ImDDqZPqrvFUa4CJ1Yj76A==" 
encryptedVerifierHashValue="lNUf5bcvc9Qi+6abbzL6MuNjqlyUukG0+G6CGgSiF3QGfhvUgaFtkWIa9nnRrEnsSvNKTdpFLgD7fCppEZcwzQ==" 
encryptedKeyValue="CNDXm+nlmbdPnEqo/CMAm0MscB/EScwfV/Vj/G/CxcQ="/>
```

We ran **`John the Ripper`** on the excel hash but after 28 hours we gave up on it.

We found some interesting information about [backdoor excel password decryption](https://hitcon.org/2015/CMT/download/day1-a-r1.pdf) It seems complicated but maybe it's the key to solving this. 

A hint was released for this challenge. **`The password is only alphabetic characters (A-Z, a-z). No numbers, no special characters, no spaces.`**

## Solution

We grepped the **`rockyou.txt`** file for only passwords with letters and created a new wordlist to use with **`John the Ripper`**. 

<p align="left">
  <img height=300 img src=./readme_assets/john.PNG/>
</p>

After 8 hours it finally gave us the password **`hsppyhsppyjoyjoy`**

Using the password we are able to open the excel file and get the flag.

## Flag

**`poctf{uwsp_j3_p3n53_d0nc_j35_5u15}`** 






# Secret Code, 186 solves, 50 points)

## Introduction

<p align="left">
  <img height=300 img src=./readme_assets/secret-challenge.PNG/>
</p>

## Solution

From the description we can assume that **`snub_wrestle`** is the **`xor key`**. What we have to do is to **`xor`** the encrypted flag with this key. After some confusion and trial and error it turned out that the colons needed to be removed, so the first byte would be 0x11 rather than 0x01. After this the remaining part is straight forward.

Converting **`snub_wrestle`** to hex = **`73 6E 75 62 5F 77 72 65 73 74 6C 65`**

We need to xor **`each character`** of the original flag string with **`each character`** of the secret key snub_wrestle so we need a for loop.

```
encrypted_message_hex = "110d01042413420b540033091c5e1e3d2a272d161d010e3a043c10110b1b1b0b1409"

xor_key = "snub_wrestle"

encrypted_message = [int(encrypted_message_hex[i:i+2], 16) for i in range(0, len(encrypted_message_hex), 2)]

key = [ord(char) for char in xor_key]

decrypted_message = []

for i in range(len(encrypted_message)):
    decrypted_char = encrypted_message[i] ^ key[i % len(key)]
    decrypted_message.append(decrypted_char)

decrypted_message = ''.join([chr(char) for char in decrypted_message])

print("decode", decrypted_message)
```
Run the code and we get our flag.

## Flag

**`bctf{d0n't_lo0k_uP_snub_wResTling}`**

## Tools

- ***`Python`***
- [RapidTables](https://www.rapidtables.com/convert/number/ascii-hex-bin-dec-converter.html)






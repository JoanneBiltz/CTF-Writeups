# Dialtone (warmup, 945 solves, 50 points)

## Introduction

<p align="left">
  <img height=400 img src=./readme_assets/dialtone-challenge.PNG/>
</p>

## Solution

The file is a `.wav` with a long string of dial tone sounds. I ran the `.wav` through a [DTMF Tones Detector](http://dialabc.com/sound/detect/index.html) and got the following string of numbers: 

`13040004482820197714705083053746380382743933853520408575731743622366387462228661894777288573`

This is obviously not alphabet substitution (a-z, 1-26). Not sure what it is.

Used a [dialtone decoder](https://github.com/ribt/dtmf-decoder) from github to see if the results were the same and they were. 

Did some googling and found that the big integer can be the issue. Convert the `BigInt` number to `hex` using [Big number converter](https://www.mobilefish.com/services/big_number/big_number.php) then from `hex` in [CyberChef](https://gchq.github.io/CyberChef/).

## Flag

**`flag{6c733ef09bc4f2a4313ff63087e25d67}`**

## Tools

- `base64`
- [DTMF Tones Detector](http://dialabc.com/sound/detect/index.html)
- [Big number converter](https://www.mobilefish.com/services/big_number/big_number.php)
- [CyberChef](https://gchq.github.io/CyberChef/)



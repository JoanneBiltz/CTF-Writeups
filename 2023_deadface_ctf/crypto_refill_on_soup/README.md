# Refill on Soup (crypto)

## Introduction

<p align="left">
  <img height=700 img src=./readme_assets/refill-challenge.PNG/>
</p>

> How could we have missed this?? There were TWO word searches stuck together that the DEADFACE courier dropped. We’ve already solved the first one, but maybe solving this second word search will help us uncover the secret message they’re trying to covertly relay to the other members of DEADFACE. Hopefully, THIS will tell us how they plan to execute their next move.

> Submit the flag as flag{TARGETNAME} (e.g., flag{THISISTHEANSWER})

You are given a word search puzzle to solve

<p align="left">
  <img height=500 img src=./readme_assets/Deadface_Word_Search_Part_2.png/>
</p>

## Solution

Solve the word search and you get the leftover letters: .
`NVAVAOLSHZASP UL MVYAOLMS HNHUZDLY AOHANVL ZPUZPKL AOLIYHJ RLAZZAVW NQWKDDEV WZLZTJNTH XSKEADVUC BVTR KLHSW EEBGBDTH HZAOLFMSFHJYVZZ`

Use [Vignere cipher](https://www.dcode.fr/vigenere-cipher) to decode text:
`GOTOTHELASTLI NE FORTHEFL AGANSWER THATGOE SINSIDE THEBRAC KETSSTOP GJPDWWXO PSESMCGMA QLDXTWONV UOMK DEALP XXUZUWMA ASTHEYFLYACROSS`

Reformatted `GOTO THE LAST LINE FOR THE FLAG ANSWER THAT GOES INSIDE THE BRACKETS STOP ASTHEYFLYACROSS`

## Flag

**`flag{ASTHEYFLYACROSS}`**

## Tools

- [Vignere cipher](https://www.dcode.fr/vigenere-cipher)






# Missing and Missed (crypto, 273 solves, 300p)

## Introduction

<p align="left">
  <img height=700 img src=./readme_assets/missing-challenge.PNG/>
</p>

## Task analysis

We are given ciphertext to decode: 
> **`++++++++++[>+>+++>+++++++>++++++++++<<<<-]>>>>++++++++++++.-.------------.+++++++++++++++++.--------------.+++++++++++++++++++++.------.++.----.---.-----------------.<<++++++++++++++++++++.-.++++++++.>>+++++++++.<<--.>>---------.++++++++++++++++++++++++.<<-----.--.>>---------.<<+++++++++.>>---------------.<<---------.++.>>.+++++++.<<--.++.+++++++.---------.+++++++..----.>>++++++++.+++++++++++++++.`** 

## Solution

I recognize the ciphertext from a previous CTF as the BrainFuck language.
Using [dcode.fr](https://www.dcode.fr/brainfuck-language) we find our flag.

<p align="left">
  <img height=300 img src=./readme_assets/bf.PNG/>
</p>

## Flag

**`poctf{uwsp_219h7_w20n9_02_f0290773n}`**

## Tools

- [dcode.fr](https://www.dcode.fr/brainfuck-language)


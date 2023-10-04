# A Tangled Web We Weave, (reversing, 105 solves, 200p)

## Introduction

<p align="left">
  <img height=700 img src=./readme_assets/tangled-challenge.PNG/>
</p>

We are given a link to an **`assembly language`** file.

## Task analysis

Read the **`assembly language`** code and reverse the steps to decrypt the flag.

Encoded message: **`db 0x0F, 0x10, 0x1C, 0x0B, 0x19, 0x04, 0x0A, 0x08, 0x0C, 0x0F, 0x20, 0x14, 0x4E, 0x11, 0x46, 0x20, 0x14, 0x4F, 0x11, 0x46, 0x20, 0x46, 0x4F, 0x48, 0x20, 0x11, 0x4F, 0x48, 0x17, 0x4E, 0x11, 0x46, 0x20, 0x4F, 0x11, 0x20, 0x12, 0x4C, 0x02`**

## Enumeration
```
section .data
    encoded_message db 0x0F, 0x10, 0x1C, 0x0B, 0x19, 0x04, 0x0A, 0x08, 0x0C, 0x0F, 0x20, 0x14, 0x4E, 0x11, 0x46, 0x20, 0x14, 0x4F, 0x11, 0x46, 0x20, 0x46, 0x4F, 0x48, 0x20, 0x11, 0x4F, 0x48, 0x17, 0x4E, 0x11, 0x46, 0x20, 0x4F, 0x11, 0x20, 0x12, 0x4C, 0x02

section .text
    global _start

_start:
    mov ecx, 0
    mov edi, encoded_message
    find_length:
        cmp byte [edi], 0
        je print_message
        inc ecx
        inc edi
        jmp find_length

    print_message:
        xor esi, esi
        mov edi, encoded_message
        decode:
            xor eax, eax
            mov al, byte [edi + esi]
            xor al, ; something missing?
            mov byte [edi + esi], al
            inc esi
            cmp byte [edi + esi], 0
            jne decode

        mov edx, ecx
        mov eax, 4
        mov ebx, 1
        mov ecx, encoded_message
        int 0x80

    mov eax, 1
    xor ebx, ebx
    int 0x80
``` 

I am unfamiliar with assembly code so it took some time to get VScode to run the program. It gave me errors so I looked closer at the code and see the problem.

<p align="left">
  <img height=300 img src=./readme_assets/error.png/>
</p>

## Solution

You can see in the code that the program used xor on the flag. First I reformatted the hex. 

**`0F 10 1C 0B 19 04 0A 08 0C 0F 20 14 4E 11 46 20 14 4F 11 46 20 46 4F 48 20 11 4F 48 17 4E 11 46 20 4F 11 20 12 4C 02`**

Then I used [CyberchefOnline](https://gchq.github.io/CyberChef/) to bruteforce the flag using xor.

<p align="left">
  <img height=300 img src=./readme_assets/xor.PNG/>
</p>

In the end this challenge was much easier than expected.

## Flag

**`poctf{uwsp_k1n9_k0n9_907_n07h1n9_0n_m3}`**

## Tools

- **`VScode`**
- [CyberchefOnline](https://gchq.github.io/CyberChef/)


# My Daily Macros (reverse engineering)

## Introduction

<p align="left">
  <img height=700 img src=./readme_assets/daily-challenge.PNG/>
</p>

> DEADFACE has gotten hold of the HR departments contact list and has been distributing it with a macro in it. There is a phrase the RE team would like for you to pull out of the macro.

You are given an Excel document.

## Solution

Excel documents are archives which can be unzipped using 7zip.

<p align="left">
  <img height=500 img src=./readme_assets/daily-unzip.PNG/>
</p>

Looking at the files you find `vbaProject.bin`

Using strings you find the flag.

## Flag

**`flag{youll_never_find_this_}`**

## Tools

- **`strings`**




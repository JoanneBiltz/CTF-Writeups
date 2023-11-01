# Wimble (forensics, 808 solves, 50 points)

## Introduction

<p align="left">
  <img height=400 img src=./readme_assets/wimble-challenge.PNG/>
</p>

## Solution

Using `file` on the downloaded file gives us: `fetch: Windows imaging (WIM) image v1.13, XPRESS compressed, reparse point fixup`

<p align="left">
  <img height=200 img src=./readme_assets/wimble-file.PNG/>
</p>
 
Windows Imaging Format (WIM) is used for the creation and distribution of disk image files. 

Tried a tool to read the .pf files [WinPrefetchView](https://www.nirsoft.net/utils/win_prefetch_view.html#:~:text=WinPrefetchView%20is%20a%20small%20utility,are%20loaded%20on%20Windows%20boot). Windows Prefetch did not give me the ability to search within all of the files and directories. 

I installed [PECmd.exe](https://github.com/EricZimmerman/PECmd) and .NET 6 to give that a try.

Ran `PECmd` in the windows CLI and output the results to a txt file.

<p align="left">
  <img height=300 img src=./readme_assets/fetch-cmd.PNG/>
</p>

Open the resulting text file and search for "flag{" will give you the flag.

## Flag

**`FLAG{97F33C9783C21DF85D79D613B0B258BD}`**

## Tools

- [WinPrefetchView](https://www.nirsoft.net/utils/win_prefetch_view.html#:~:text=WinPrefetchView%20is%20a%20small%20utility,are%20loaded%20on%20Windows%20boot)
- [PECmd.exe](https://github.com/EricZimmerman/PECmd)



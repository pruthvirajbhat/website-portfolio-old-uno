---
layout: post
title: Pickle Rick
subtitle: beginner CTF
tags: [CTF, THM]
odate: 01-06-2022
fdate: 08-06-2022
pdate: 08-06-2022
---

### Scanning
When the machine gets started, barely any info is provided. Network scanning using Nmap is run on the machine to know more. Port 22 (ssh) and 80 (HTTP) are open. Since HTTP is open, the ip is enumerated by checking it on browser to know more. The homepage has an image and some some instructions: Gain access to Rick's Computer by logging in and get those 3 ingredients that are the flags.

### Enumeration
Viewing the source code, gives username: **R1ckRul3s** \
To view all directories and files on the webserver, gobuster is used to bruteforce check them all. Obtained files include login.php, index.html and robots.txt \
Going to each page to check the files, there are some data provided in robots.txt >> **Wabalabadubdub** :: which might be the passwd. Other places like assests directory and index.html - there are not much interesting in these files. \
For more possible enumeration apart from gobuster, could have run dirb or nikto. 
Going into the login page with username and possible passwd, it logs in!

### Exploitation
OK

Now, there's a command panel which looks like when commands are provided it will execute them. Listing all files provides many files.

```
Sup3rS3cretPickl3Ingred.txt
assets
clue.txt
denied.php
index.html
login.php
portal.php
robots.txt
```

Using `cat` command is not possible as it looks like it's been disabled. But not `less` \
`less Sup3rS3cretPickl3Ingred.txt` >> **mr. meeseek hair** \
That's the first Ingredient.

`less clue.txt` >> `Look around the file system for the other ingredient`

Looking around, there's another user called rick. Commands like `ls -alh /home/rick` gives another txt file 'second ingredients'. `less '/home/rick/second ingredients'` >> **1 jerry tear**\
That's the second ingredient.

Just to be sure, `sudo -l` command was run to check the permission status of the user. Observations:\
`(ALL) NOPASSWD: ALL` - so sudo can be run.

Looking at what's in root folder is the first step after gaining/finding out super user privileges.

`sudo ls -la /root` >> there's the third file `3rd.txt` \
`sudo less /root/3rd.txt`  >> 3rd ingredients: **fleeb juice**

Ufff! All 3 flags has been captured and challenge completed.
<!--Comment looks like this-->
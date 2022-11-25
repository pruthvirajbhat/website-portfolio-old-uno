---
layout: post
title: few THM linux challenges
subtitle: tryhackme, other exercises
tags: [linux, THM]
odate: 27-04-2022
fdate: 20-05-2022
pdate: 30-05-2022
---
```
Challenges Level: Easy
```
__TL;DR__: Doing numerous tryhackme rooms, online CTFs and textbook reading to get the foundations right & clear

After working on [bandit overthewire](/2021-05-17-bandit-challenge/), the sky was the limit to work on this topic for a while. There are many places to learn Linux from. It's free in every sense of the word and so are the resources to learn and use. Numerous rooms are dedicated on _tryhackme_ for Linux. There's a textbook called [_Linux Basics for Hackers_ from OccupyTheWeb](https://booktree.ng/download/linux-basics-for-hackers/) which was a great resource for security POV learners/enthusiasts. It's important to get a POV for learning such a big topic like Linux. The sheer knowledge for Linux is as deep as the Pacific and it's easy to get lost in the ocean. 

The book goes into great detail for learning simple commands for the first time. But they can also be learnt as and when practical work, CTFs are done. So after finishing a round of reading, got started with working on tryhackme rooms: 

1. [regex](#regex) 
2. [linux strength training/reinforcing](#linux-strength-training) 
3. [linux modules](#linux-modules) 

### [regex](https://tryhackme.com/room/catregex)
regex breifly provides all the basics of each format type of values that need to be used to find respective type of characters.
Each room has it's own fair share of questions that demand usage of all the material provided to help get the flag. 

#### [Linux Strength Training](https://tryhackme.com/room/linuxstrengthtraining)

Linux Strength Training reaffirms competitors' Linux knowledge w/ study material for reference/help. Task 1&2 is present for revising (catching up the competitors' knowledge). Task 3 - Directory traversal is focused under revision. It's just like breathing, it's required. 

find command is extensively made to be used to get familiar with it. File names with respective charactristics are provided and they have to be searched and read to get to know what the next step is. 

Task 4 - Hashing is a consistent concept used to check the integrity of a message. It's a one way method, where after the message is hashed, it is nearly impossible to obtain the message from the hash. With Hash Algorithm like MD4, MD5, SHA-1, SHA-2, SHA-256, RIPEMD-160, Whirlpool, NTLM, LANMAN and many dozens more. Using John the Ripper, hashes are brute-forced with respective provided wordlist on the ssh machine to crack the hash.

Task 5 - [base64](https://www.base64encode.net/) binary to ASCII encoding scheme is talked about. Which means elsewhere in the tasks, there's some incomprehensible data that can be base64 encoded.

Task 6&7 - Encryption and decryption using gpg command. Encryption is a process used to conceal a message, for confidentiality purposes. It can be encrypted using mathematical algorithms. It differes from Hashing, since the encrytped message can be used to decrypt it to get the original message back. The system tool gpg can be used for encrytpion and decryption. From the man page of gpg:

```
gpg  is  the  OpenPGP part of the GNU Privacy Guard (GnuPG). 
It is a tool to provide digital encryption and signing services using the OpenPGP standard.
```

The text file needs to be provided w/ a cipher algorithm when passing it w/ `gpg` for encrytion with the file (password is passed while encypting, which is required for decryption also if system is rebooted).A new file, with encrypted message has a .gpg extension. It can be decrypted with gpg command. \
John is used again to brute-force crack encrypted data using `gpg2john` to create hash of password. It's then run with wordlist to get password.  

Task 8 - Reading Database using mySQL service. mysql service is started to read the database and answer the respective questions to find the flag.

Final Task 9 - is a challenge where questions posed make use of all the concepts covered in previous tasks and each task provides instructions for the next to obtain respective flags. Chat reading from logs provide data about a file w/ respective characteristics. It's read to obtain flag and further instructions. An enrypted file is seen and it needs to be decrypted to get the password of the file. Then sql database is seen where the next user's password is stored. using mysql service, the database is read to obtain the password of the final user. Logging in as root of the user and reading the text file in root dir - the final flag is obtained and the room in complete. 

#### [Linux Modules](https://tryhackme.com/room/linuxmodules)
Commands covered are disk usage (du), grep, String Operation Commands like tr, awk, sed, xargs, curl, wget, xxd; other commands like tar, gpg, id/pwd/uname, ps/kill, file/stat, netstat, less, more, diff, uniq, export, reset, system/service are briefed. 

#### Inference
All the modules seem easy and workable, providing better options and functionality dealing with big data to make user's life easier while parsing. 

---
layout: post
title: Bandit OverTheWire
subtitle: beginner-level linux challenge
tags: [linux]
odate: 29-03-2022
fdate: 24-04-2022
pdate: 27-04-2022
---
```
Challenge Level: Easy
```
Bandit challenge from OverTheWire introduces what a simple challenge is to a beginner. It's about Linux, and prepares how to be effective with it. The goal is simple: there's Instruction in every level, follow through to get the flag viz the passowrd for the next level. Each level has instruction on particular subject. Complexity of instructions increases with level.

This write-up is focused on *what*s rather than the *how*s. The challenge is seen more like a stepping stone to understanding how linux commands are used in action. The contents can be seen as:
1. [Write-up](#write-up)
2. [Inference](#inference)

## Write-up
Using ssh, machine is accessed at the start - Level 0. At the beginning, basic file management and file manipulation commands are used. Commands include _ls_, _pwd_, _cat_, _cd_ and _find_ is used. I took more time with find command and it's options.

Specificity in the instructions compels to look into options of each command.

From Level 7, it's seeing internal file data and manipulationg it to display it to user's whim. Using commands like _sort_ and _grep_. Data that's encoded by _base64_ or encrypted with _rot13_ are decoded or decrypted using relavent commands to get the flag. There's a _hexdump_ on Level 12 which needs to be reversed. Then it turns out to be compressed or zip filed multiple times using commands like _gzip_, _bzip2_ and _tar_. The file type must be observed and relavant command must be used to get the flag by decompressing it multiple times.

At Level 13, login via ssh private key is done into Level 14, and entering into a machine by submitting data (also using ssl encrytion) to a localhost, using commands like *nc* and *ncat*. Later checking on different ports to see which of them are open (using *nmap*) and speaking ssl. The one that does provides RSA private key as flag for the next level 17.

Login to Level 17 using RSA private key, where difference in data among 2 files end up being the flag for the next level.

Level 18 shows that connecting to the shell is not possible normally even with password, which compels user to force open up the terminal for the level. options for ssh command is explored and seen.

Level 19, ssuid binary file is executed to look into file system as the next user bandit20 to get the flag. running the file shows that userID is set to be bandit20 to access the file.

Level 20, needs to be done with 2 simulatenous sessions. One session with outputting level20 password using nc onto localhost on a known port. Another session with the bin file that connects to localhost on a port, when outputting data matches with data seen by bin file run on known port -> it sends the flag.

Level 21 _cron_ job scheduler is used to automatically execute a program. It's seen what the command is doing and following the process where it executes a script and the script dumps the flag into a temp file will lead to displaying the flag. The next level, the script file commands must be executed step-by-step to get the flag.

Level 23 nudges to create a _shell script_ to display the flag. The cronjob executes scripts written in a dir. A tmp dir is made and a script is written to pass/display the flag -- and that's how it's obtained.

Level 24 had the requirement to write a shell script for executing a bruteforce attack on a daemon listening on port 30002 for next level passwd

Level 25 has a different shell for the user. So it can't execute the ssh key to get into the next level. Instead the file is executed to get into the more window. Here, the window is shrunk and the entire output is not visible. Partly shown output window is misused to access the editor window of vim. Here, the editor window acts as a shell. Commands can be executed in command line text editor to get into Level 26 by setting/spawning bash as the shell. Shell for Level 26 appears. Level 26 has the jailed shell. Listing files there's a SUID, run it to get the flag for Lvl27.

Level 27 is cloning a repo using _git_ command and checking out the file gives the flag. 28 checking out the log, seeing previous commits provides the flag. 29 checking out different branch gives the flag. 30 checking out the tags gives the flag. 31 creating specific file with specific contents to a remote repo. after add, commit and push -> the flag is provided as the output.

Level 32 challenge can be solved by changing the shell environment variable, to access bash as default shell.

## Inference
Most of the basic commands used IRL are covered and explored in this challenge. It's great for a beginner to get used to linux CLI and further encourages to move on in a gamified manner with the progression of the activity.
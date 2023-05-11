---
layout: post
title: 25DaysXmas2020 - Day 24 - Last Day 
subtitle: Final Challenge
tags: [THM]
odate: 19-05-2022
fdate: 19-05-2022
pdate: 19-052022
---

Final Room, the final challenge

Day 24 `Final Challenge`
Materials: client side filters, shell upgrade and stabilize, mysql client, priv esc w/ lxd
Scanning by nmap, gobuster, pass an exploit in attackbox db as jpeg extension file but php script to open reverse shell. Use nc to listen on specific port and get a rev shell. Then horizontal priv esc from mysql client to find the particular user with creds in a db. Login to other user, observe vulnerability i.e., lxd and priv escalate using that vuln (as provided in the day's materials) and obtain root shell.
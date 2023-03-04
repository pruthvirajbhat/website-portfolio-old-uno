---
layout: post
title: Operation Softcell
subtitle: collective attack on telcoms
tags: [tracelay-writeup]
odate: 20-12-2022
pdate: 31-12-2022
---
# Operation Softcell

An advanced persistent attack targeting/campaigning against Telecommunication (telco) providers has been active since 2012 and this attack is dubbed **Operation Soft Cell** by Cybereason researchers.

With more than 8 billion subscriptions today - it is considered as critical infrastructure. And attack on telcos have quadrupled since the last 13 years. According to fiercetelecom.com report
- 30% of telco providers reported sensitive customer information stolen
- 23% of critical infrastructure was hit by nation state
- 60% of critical infrastructure are most worried about cyber threats

Data obtained are Call Detail Registries - metadata of calls and messages of telcom customers which are highly valuable to threat actors and APTs to gain intel of an individual without exploiting them directly. Metadata from CDR include date of call, time of call, call duration, originating number, terminating number, IMEI - International Mobile Equipment Identitiy and CI - Cell Site Identity Number.

Operation Soft Cell is considered to be an espionage-motivated attack, since the tools used in the attack are modified and highly-customized. Cybereason believes with high certainity that the attack is backed by the Chinese government. That’s because the bad actors used a unique set of tools like china chopper web shell, Poison IVY RAT, hTran, mimikatz to ultimately exfiltrate credentials that are often associated with the Chinese government-backed group, APT10.

## What was done
This multi-wave attack spanned at least six years and over the course of that time the group was able to obtain over 100GB of call record data on over 200 million entities, including call and messaging logs, device information, and tower location data which could provide the physical location of the phone and its owner. This data, while not providing information on the content of calls and messages being sent, could provide a detailed picture of a person’s movements and personal network.

## How did they operate?
To gain initial access to the network, the attackers used a code injection attack by exploiting a vulnerability in poorly written code within the network infrastructure. Once executed, the attackers had complete control over the network. They used this access to steal private data over a number of years, however, it could have been used to do even worse - they could have shut down service altogether if they wanted to.

Their Modus Operandi is go low and slow. They go under the radar - usually the mark of a persistent attacker. Cybereason solutions and defense teams kept blocking them and attackers kept coming back.
One such attack was detected in 2018. After the solution was implemented in the victim network. The attack duration happened to occus over 9 months to a year.

- first wave happened with web shell activities, credential theft with RATs deployed like plugx, poisonivy (PIVY). recon from nbt scan suggests the attack was conducted by a Nation State 
- second wave (2 months later) - a modified version of original webshell was implemeted, attempted credentials stealing (and blocking by cybereason solution), recon activity - to gain network infrastucture data, many out-of-the-box binaries (like reg.exe for gaining SAM hives containing password hashes) and data exfil using PIVY, hTran and web shells 
- third wave (3 months later) - new webshell, user enumeration, gained domain admin privileges, lateral movement, connection bouncer/proxy, data exfil, containment actions - activity is also widely spread across network to access more information
- fourth wave (1 month later) - Same tools, different IOCs; attackers create VPN access, AD enumerations - complete data exfiltration done by compression of data using winrar tool and abusing existing binaries (like certutil.exe as a downloader) on OS

At the final wave, activity done due to their prime motivation was observed. Active Directory enumeration was done same way as seen in 2nd Wave, but data exfiltration was the prime motivation to perform such an activity - hence confirmed that this was a nation state threat actor 

Methodology Used to track the attack
1. IOC Inventory - any hashes, filenames, domains, registry keys obatained are all updated in repositories and database is created - larger the attack scope - larger the data obtained
2. Hunting for known evil - automatic and manually done - against affected and all other customer environments - will know the scope of the attack and how many machines must be triaged
3. threat actor arsenal - their tools, rev engg them - most tools are available for free - on github or other hacking forums - analyzing the modified tool pinpoints the group
4. behavioural profile - MITRE ATT&CK F/w - key factor in Threat hunting 
5. operation activity - reconstruct the C2 infrastructure, analyze activity patterns to gain more specific intel (like time) on group of operation geographically
6. suspects - very careful about the attribution - decided that it's chinese (after analyzing the tools, techniques, infrastructure, motives)

## Safety Measures
It's very difficult to "seal the gates" - since APTs will find one way or another. So, 100% safety isn't guranteed. What can be done, is validate that the current Infrastructure is clean: Proactively hunt

1. Practicing Defense-in-depth (layered security mechanisms, redundancies, fail-safe defense processes, Web Application Firewalls) is the one of the best ways to ensure safety from APTs, including a focus on both host-based and network security.
2. Latest detection and prevention capabilities with behavioral analysis must be in place to detect new modified forms of attack
3. Resources that share IT network and OT network must be monitored

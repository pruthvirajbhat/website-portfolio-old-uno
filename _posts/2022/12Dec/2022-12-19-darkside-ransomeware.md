---
layout: post
title: packet capture and analysis
subtitle: learning more about packet contents
tags: [Network]
odate: 19-12-2022
pdate: 29-12-2022
---
# DarkSide Ransomeware
DarkSide Ransomware first made it's appeareance in August 2020 is associated with DarkSide group probably based in Eastern Europe, probably Russia. Notorious since they are believed [to be used behind the colonial pipeline attack](https://www.bankinfosecurity.com/fbi-darkside-ransomware-used-in-colonial-pipeline-attack-a-16555) (even though the group denied charges quote "Our goal is to make money, and not creating problems for society"), they target their victims using ransomware and extortion and operate while providing Ransomware-as-a-service (RaaS).

The team is highly active on their forums and update with their customers related to the ransomware. They have a phone number and a help desk to facilitate negotiations with victims. While gaining techincal knowledge about the victim before an attack, they also collect general information about the company - revenue, size and practices.

Similar to other ransomware variants they have double extortion trend which is while they encrypt user data, they exfiltrate the data to threaten to make it public if ransom isn't paid rendering the strategy of backing up of data useless. They have released more than 40 companies' confidential data and demand ransom ranging from USD 200,00 to USD 2,000,000.

## Group's Motives
The group appaears to also have "rules" that prohibit attacking schools, universities, oldage homes, hospitals, non-profit organizations and state bodies. They prohibit attack on products that causes reputational damages. Attack on Commonwealth of Independent States (CIS) is prohibited. Customers are prohibited to use the product on other locations. Account maintained by one entity with the group must not be shared/transfered with third parties. 

They also make a point donating money in BTC to different charities and make a show of posting donation receipts on their forums.

Points to note:
- Relatively new group that has gained a reputation of being "professional" and "organized" in a short span of time.
- Severity assessment places them at "High" Threat Level given the attack potential to be destructive.
- exploitation of public facing apps, lateral movement in the network and targeting Domain Controller to gain data from compete network enviroment  

After gaining intel about the company, they are checked if they qualify as a posssible target with respect to the group's code of conduct. If yes, they move to the next stage.

## Technical Aspects/Details of Operation
### Gaining Access
Gaining access to the network by attackers are very sophisticated - by exploiting the public-facing applications (like RDP), Privilege Escalation and Impair Defenses. The Ransomware exploits vulnerabilities like CVE-2019-5544 and CVE-2020-3992. Both have widely available patches, but the attack group targets organizations who are unpatched or using older software versions.

### Downloading the ransomware
Powershell is used by the attackers to download the ransomware binary as "update.exe" using "DownloadFile" command. The binaries certutil.exe is abused in the process of downloading the ransomware binary. Temporary binaries and files are also downloaded, and a shared folder created on the infected machine for lateral movement.

### Taking control of Domain Controller
1. Lateral Movement and Data Exfiltration
Lateral Movement is done with the sole goal of acheiving control over Domain Controller. At the Domain controller, they gain sensitive intel from Security Account Manager hive which stores targets' passwords.

2. Maximize damage on all systems
On the Domain Controller, binary file is downloaded from infected system using bitsadmin.exe via powershell to further attack more systems on network. A scheduled task is created to execute the ransomware.

### Malware Analysis
On analysis, the DarkSide ransomware collects the information about computer name and system language in its initial code execution using GetSystemDefaultUILanguage() and GetUserDefaultLangID() functions.

DarkSide is used to target English-speaking countries. DarkSide ransomware checks the default system language and won't encrypt files if the langauge code is Russian (419), Ukrainian (422), Belarusian (423), Armenian (42B) - languages mostly from Eastern Europe and CIS countries. 

It proceeds to stop services related to security and backup solutions like vss, sql, backup, etc and creates a connection with (command and control) C2 server. 

### Impair Defenses and Malware execution
It creates a powershell process launching a script that terminates different processes that can unlock files. Then it steals the data stored and encrypts them. 

A unique userID string is created, icons of files changed and an intuitive wallpaper with instruction to open README.{userID}.TXT file.

### Safety Measures
- Optimize existing security solutions 
	- lockout policies to counter bruteforce logins, 
	- tough and unique passwords for login, 
	- deploy Multi-Factor Authentication (MFA), 
	- minimum priviliges granted to users according to their function
- Use VPN to access network. Turn off RDP if not used. Atleast change the RDP port to a non-standard port
- Keep systems patched
- Regular Backup
- Enable a Next Generation AntiVirus with Anti-malware or anti-ransomware features that offer latest solutions.

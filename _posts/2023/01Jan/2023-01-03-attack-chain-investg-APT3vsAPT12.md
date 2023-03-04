---
layout: post
title: Create an Investigation of attack chain for APT3 & APT12
subtitle: Investigation report on Attack chain of APT3 & APT12, plus comparison
tags: [tracelay-writeup]
odate: 03-01-2023
pdate: 03-01-2023
---
The Matrix is built for security providers' understanding of the different unintelligble aspects of a Threat - Capability, Opportunity and Intentions

Defenders can understand what opportunities are available since they might be the target. But when each move of an attacker is mapped in different stages - one can understand their attacker's capabilities and intentions.

The Matrix is made by MITRE, a non-profit organisation established to provide security solutions. Adeversial Tactics, Techniques and Common Knowledge (ATT&CK) framework are guidelines for classifying and describing cyberattacks and Intrusions. The tactics (what the attacker does) are listed below:

1. Reconnaissance
2. Resource Development
3. Initial Access
4. Execution
5. Persistance
6. Privilege Escalation
7. Defense Evasion
8. Credential Access
9. Discovery
10. Lateral Movement
11. Collection
12. C2
13. Exfiltration
14. Impact

Techniques (how the attacker does it) are listed in detail and common_knowledge/procedure further provide how the technique was utilised in detail.

Above the first row in each Coloumn has the tactics listed. But since this ATT&CK framework is v12.1 it's highly detailed if viewed completely. So breaking down of each matrix with respective coloums sequentially is done for each APT.

Then both APT3 and APT12 TTPs are compared, with the common techniques and procedures of each APT are given a higher priority for the enterprise security teams to focus on.

---
## APT3

![](../../../assets/images/apt3vapt12/apt3.svg)
Breaking down each of the parts of the matrix if APT32 we have the first 4:
Reconnaissance, Resource Development, Initial Access and execution

![](../../../assets/images/apt3vapt12/apt3_1.png)

then the next 3 highly employed tactics and techniques: 
persistence, privilege escalation, defensive evasion and credential access

![](../../../assets/images/apt3vapt12/apt3_4a.png)

![](../../../assets/images/apt3vapt12/apt3_4b.png)

![](../../../assets/images/apt3vapt12/apt3_4c.png)

Focusing on the remaining Defensive Evasion techniques

![](../../../assets/images/apt3vapt12/apt3_4d.png)


the other tactics and techniques for the APT32 are
Discovery, Lateral Movement, Collection, Command and Control

![](../../../assets/images/apt3vapt12/apt3_2.png)

finally there's exfiltration and Impact

![](../../../assets/images/apt3vapt12/apt3_3.png)

---
## APT12

![](../../../assets/images/apt3vapt12/apt12.svg)

Breaking down each of the parts of the matrix if APT28 we have the first 4:
Reconnaissance, Resource Development, Initial Access, Execution

![](../../../assets/images/apt3vapt12/apt12_1.png)

then the next 3 highly employed tactics and techniques: 
persistence, privilege escalation, defensive evasion and credential access

![](../../../assets/images/apt3vapt12/apt12_4a.png)

![](../../../assets/images/apt3vapt12/apt12_4b.png)

![](../../../assets/images/apt3vapt12/apt12_4c.png)

Focusing on the remaining Defensive Evasion techniques (APT12 seems to be very selective in their techniques.)

![](../../../assets/images/apt3vapt12/apt12_4d.png)


the other tactics and techniques for the APT28 are
Discovery, Lateral Movement, Collection, Command and Control

![](../../../assets/images/apt3vapt12/apt12_2.png)

finally there's exfiltration and Impact

![](../../../assets/images/apt3vapt12/apt12_3.png)

---
## Comparing APT3 vs APT12 TTPs
TTPs of APT3 are colored in red.
TTPs of APT12 are colored in yellow.
TTPs of both APT3 and APT12 are colored in green.

![](../../../assets/images/apt3vapt12/layer_by_operation.svg)

Zoomed in parts of ATT&CK matrix with both APT32 and APT28
we have the first 4:
Reconnaissance, Resource Development, Initial Access, Execution

![](../../../assets/images/apt3vapt12/comp_1.png)

then the next 3 highly employed tactics and techniques: 
persistence, privilege escalation and defensive evasion
![](../../../assets/images/apt3vapt12/comp_4a.png)

![](../../../assets/images/apt3vapt12/comp_4b.png)

![](../../../assets/images/apt3vapt12/comp_4c.png)

Focusing on the remaining Defensive Evasion techniques

![](../../../assets/images/apt3vapt12/comp_4d.png)

the other tactics and techniques for the APT3 vs APT12 are
Credential Access, Discovery, Lateral Movement, Collection, Command and Control

![](../../../assets/images/apt3vapt12/comp_2.png)

finally there's exfiltration and Impact

![](../../../assets/images/apt3vapt12/comp_3.png)


## Conclusion
Mapping all TTPs of APT3 and APT12 are done hence creating an Investigation report of their attack chains.

Each individual TTPs mapped for respective APTs can be a source of reference for red teams for red teaming and adversary emulation activities.

It's also very useful for gap assessment for the security team to get started on -> common TTPs can be prioritized first
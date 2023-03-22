---
layout: post
title: brief note on Sigma and Yara rules
subtitle: Sigma and Yara rules
tags: [tracelay-writeup]
odate: 02-02-2023
pdate: 22-03-2023
---

Threat hunting is a proactive approach to cybersecurity that involves searching for signs of malicious activity within an organization's network. One of the tools that security professionals use in their threat hunting efforts are Sigma rules and Yara rules.

Sigma is a tool for the open sharing and crowdsourcing of threat intelligence, it focuses on SIEM instead of files or network traffic. 

Snort is an open sourse IPS/IDS, uses rules based language combining signature, profile, anamaly inspection methods to detect malicious activity. What Snort is to network traffic, and YARA is to files, Sigma is to logs.

## Sigma Rules

Sigma is an open-source tool that can be used to detect and analyze security incidents. It uses a standardized rule format to describe various threat indicators, such as file hashes, IP addresses, and domains. These rules can be used to identify potential security threats and to create custom detections for specific use cases.

One of the key benefits of Sigma is its simplicity. The rule format is easy to understand and write, making it accessible to security professionals who may not have extensive programming experience. Additionally, Sigma has a large and active community of users who contribute new rules and provide feedback, which helps to keep the tool up-to-date and effective.

### Use Cases
- Malware Detection: Sigma can be used to detect various types of malware, such as ransomware, trojans, and worms. The tool can identify known indicators of malicious activity and provide alerts to security teams.
- Data Exfiltration: Sigma can be used to detect when sensitive data is being exfiltrated from an organization's network. This can help to prevent data loss and protect against data breaches.
- Phishing Detection: Sigma can be used to detect phishing attempts and prevent sensitive information from being stolen. The tool can identify indicators of phishing emails, such as suspicious domains and fake login pages.

Sigma rules can be converted into a search query specific to your SIEM solution and supports various solutions: Splunk, ElasticSearch Query Strings and DSL, Kibana, Microsoft Defender Advanced Threat Protection (MDATP), Azure Sentinel, QRadar, LogPoint, Qualys, RSA NetWitness, LimaCharlie, ArcSight, PowerShell and Grep.

Sigma is an open-source project with three major components:
- A language specification for the generic Sigma rule format.
- Open repository for sigma signatures with **over one thousand rules for several attacker behaviours and techniques**.
- `sigmac`, a conversion utility to generate search queries for different SIEM systems from Sigma rules.

![](../../../assets/images/sigma_yara/Sigma-description.png)

A Sigma rule is written in YAML and defines the what and the where to look in system logs. Every Sigma rule also specifies metadata such as the author of the rule, a unique rule identifier (UUID), MITRE ATT&CK techniques, and references, eg. an URL for additional information.

Taking a look at a sigma rule from the repository `rules/linux/builtin/lnx_pwnkit_local_privilege_escalation.yml` from the github repo, https://github.com/SigmaHQ/sigma.git 
This rule detects the privilege escalation vulnerability, PwnKit.

```
title: PwnKit Local Privilege Escalation 
id: 0506a799-698b-43b4-85a1-ac4c84c720e9 
status: experimental 
description: Detects potential PwnKit exploitation CVE-2021-4034 in auth logs author: Sreeman 
date: 2022/01/26 
references:
 - https://twitter.com/wdormann/status/1486161836961579020 
logsource: 
 product: linux 
 service: auth 
detection: 
 keyword: 
  - "pkexec"
  - "The value for environment variable XAUTHORITY contains suscipious content" 
  - "[USER=root] [TTY=/dev/pts/0]" 
 condition: all of keyword 
 falsepositives: 
  - Unknown 
 level: high 
 tags: 
  - attack.privilege_escalation
  - attack.t1548.001
```

## Yara Rules

Yara is a tool that can be used to scan files and identify patterns that match known malware or other security threats. Yara rules are written in a custom syntax and describe the characteristics of malicious files, such as specific strings of code, file signatures, and other identifying information.

One of the key benefits of Yara is its versatility. The tool can be used to identify a wide range of security threats, including malware, viruses, and other types of malicious software. Additionally, Yara has a large and active community of users who contribute new rules and provide feedback, which helps to keep the tool up-to-date and effective.

### Use Cases

- Malware Identification: Yara can be used to identify specific types of malware, such as Trojans, worms, and other malicious software. The tool can help security teams understand the nature and scope of an attack, and take appropriate action.
- File Scanning: Yara can be used to scan large volumes of files and identify those that match known malware signatures. This can help organizations to quickly identify and isolate infected files, and prevent the spread of malware within their networks.
- Threat Intelligence: Yara can be used to gather threat intelligence, such as the origins of specific malware samples, the techniques used by attackers, and the systems and networks that are most at risk. This information can be used to inform security strategies and to better prepare organizations for future attacks.

YARA rules are like a piece of programming language, they work by defining a number of variables that contain patterns found in a sample of malware. If some or all of the conditions are met, depending on the rule, then it can be used to successfully identify a piece of malware.

Structure of YARA rule:
```
rule MyFirstYaraRule
{
    strings:
        $my_text_string = "text here"
        $my_hex_string = { E2 34 A1 C8 23 FB }

    condition:
        $my_text_string or $my_hex_string
}
```
The word rule here is a reserved word that shows the start of a Yara rule. The string MyFirstYaraRule is the name that you choose for your Yara rule. It is a good idea to write a meaningful name to recognize it later when we are looking at the results based on multiple Yara rule hits.

The string: section defines strings (HEX strings as well) that you want to search for (usually based on your logic of identifying a malicious file). You can have as many strings as you want.

The condition: section defines the conditions that you want to check so that your Yara rules can trigger a match. The above sample rule is checking for any of the strings defined in the strings: section. However, it is not limited to this condition only. We can make our condition to match for file size, its type (such as MZ or executable), different combinations of (AND/ OR conditions), and many more.

In conclusion, Sigma and Yara rules can be powerful tools in the threat hunting process. By providing organizations with the ability to identify potential security threats and respond quickly, these tools can help to minimize the risk of data loss and protect against malicious activity.
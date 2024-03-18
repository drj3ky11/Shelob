[Source](https://www.crowdstrike.com/blog/anatomy-of-alpha-spider-ransomware/)

Developer of Alphv ransom
Written in Rust

> The events described in this blog have been attributed to ALPHA SPIDER affiliates by CrowdStrike Counter Adversary Operations

## Intial foothold

[CVE-2021-44529](https://nvd.nist.gov/vuln/detail/CVE-2021-44529) A code injection vulnerability in the Ivanti EPM Cloud Services Appliance (CSA) allows an unauthenticated user to execute arbitrary code with limited permissions (nobody)

[CVE-2021-40347 and PwnKit](https://github.com/ly4k/PwnKit) see also [Hunting pwnkit Local Privilege Escalation in Linux (CVE-2021-4034)](https://www.crowdstrike.com/blog/hunting-pwnkit-local-privilege-escalation-in-linux/)

Then a [reverse-ssh](https://github.com/Fahrj/reverse-ssh) in Go with cron daemon

## Step II

System and services discovery mainly with nmap. To gather additional credentials they have observed the use of [mitm6](https://github.com/dirkjanm/mitm6) *As DNS server, mitm6 will selectively reply to DNS queries of the attackers choosing and redirect the victims traffic to the attacker machine instead of the legitimate server* and [responder](https://github.com/lgandx/Responder) *IPv6/IPv4 LLMNR/NBT-NS/mDNS Poisoner and NTLMv1/2 Relay*

> Threat Actor 1 also attempted to exploit the vulnerability identified as CVE-2021-21972.7 CVE-2021-21972 is a remote code execution vulnerability in a vCenter Server plugin, which a threat actor may exploit to execute commands with unrestricted privileges. Later during this attack, Threat Actor 1 also installed [masscan](https://github.com/robertdavidgraham/masscan) on the compromised CSA server to perform additional network reconnaissance activities.

Next step usually is to loock for [Veeam credentials](https://github.com/horizon3ai/CVE-2023-27532), to delete backups before the ransom playload execution.

Looking for logs in *Terminal Services LocalSessionManager/Operational*

## Hiding persistance

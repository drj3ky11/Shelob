## Some sources

- [ ] [One](https://blog.talosintelligence.com/deep-dive-into-phobos-ransomware/)
- [ ] [Two](https://www.cisa.gov/news-events/cybersecurity-advisories/aa24-060a)
- [ ] [Trhee](https://medium.com/@Intel_Ops/phobos-ransomware-analysing-associated-infrastructure-used-by-8base-646560302a8d)
- [ ] [Four](https://www.fortinet.com/blog/threat-research/phobos-ransomware-variant-launches-attack-faust)
- [ ] [And much more](https://malpedia.caad.fkie.fraunhofer.de/details/win.phobos)


## Notes

Phobos is used by 8Base group

> According to open source reporting, Phobos ransomware is likely connected to numerous variants (including Elking, Eight, Devos, Backmydata, and Faust ransomware) due to similar TTPs observed in Phobos intrusions.

## Reconnaissance and Initial Access

Phishing campaigns, [Angry IP Scanner](https://github.com/angryip/ipscan) searching vunerable RDP. 

[SmokeLoader](https://github.com/vc0RExor/Quick-Analysis/blob/main/SmokeLoader/SmokeLoader.md) and an other intresting analysis [here](https://farghlymal.github.io/SmokeLoader-Analysis/)

> SmokeLoader malware decrypts its payload in three stages. The first contains many random API calls to obfuscate the execution flow, while the other two involve shellcode stored in allocated memory. The final binary is exposed in the third stage, where a binary copy of the PE (Windows Portable Executable) data in that memory block gives the final payload in its original form.

They manipulate `VirtualAlloc` or `VirtualProtect API` opening an entry point that enables to the code to be injected into running processes. It allows, also, evade network defense tools.

[SystemBC](https://www.kroll.com/en/insights/publications/cyber/inside-the-systembc-malware-server)

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

[SystemBC](https://www.kroll.com/en/insights/publications/cyber/inside-the-systembc-malware-server) uses SOCKS5 proxy as their main functionality. For an extended readin you can go to [this](https://github.com/vc0RExor/Malware-Threat-Reports/blob/main/The%20Swiss%20Knife%20-%20SystemBC%20%7C%20Coroxy/The%20Swiss%20Knife-SystemBC_EN.pdf)

> We also examined the encryption methodology used by Phobos. Versions of Phobos released after 2019 use a custom implementation of AES-256 encryption, with a different random symmetric key used for each encrypted file, instead of using the Windows Crypto API like earlier variants. Once each file is encrypted, the key used in the encryption along with additional metadata is then encrypted using RSA-1024 with a hardcoded public key, and saved to the end of the file. This algorithm has been documented before, for example in this [Malwarebytes+](https://www.malwarebytes.com/blog/news/2019/07/a-deep-dive-into-phobos-ransomware) post from 2019, and the process still remains the same.

For the User Acount Control [UAC](https://book.hacktricks.xyz/windows-hardening/authentication-credentials-uac-and-efs/uac-user-account-control) bypass (to achive elevated privileges and avoid to alert the user) they have used a vuln in the [.Net Profiler DLL](https://offsec.almond.consulting/UAC-bypass-dotnet.html). The DLL is just used to create a new process with the binary, it is written in `\Users\User\AppData\Local\Temp\SERIALNUMBER`. 


The 8base ransomware checks for file size, with a target set at 1.5MB. The ransomware fully encrypts files smaller than 1.5MB, others just partially.


Once in the victim server, they created a working directory and try to deploy some of the next tools:
- [Process Hacker](https://processhacker.sourceforge.io/) and [this](https://github.com/PKRoma/ProcessHacker) *A free, powerful, multi-purpose tool that helps you monitor system resources, debug software and detect malware.*
- [LaZagne](https://github.com/AlessandroZ/LaZagne) *open source application used to retrieve lots of passwords stored on a local computer* it could be used inside [Automim suit](https://www.crowdstrike.com/blog/how-to-test-endpoint-security-with-red-teaming/) with Mimikatz.
- [IObit](https://www.iobit.com/en/iobit-unlocker.php) to unloock files

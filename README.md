# windows10_ntfs_crash_dos
PoC for a NTFS crash that I discovered, in various Windows versions

Type of issue: denial of service. One can generate blue-screen-of-death using a handcrafted NTFS
image. This Denial of Service type of attack, can be driven from user mode, limited user account or
Administrator. It can even crash the system if it is in locked state.

**Reported to Microsoft** on July 2017, they did not want to assign CVE for it nor even to write me when they fixed it.

## Affected systems

1. Windows 7 Enterprise 6.1.7601 SP1, Build 7601 x64
2. Windows 10 Pro 10.0.15063, Build 15063 x64
3. Windows 10 Enterprise Evaluation Insider Preview 10.0.16215, Build 16215 x64

Note: these are the only systems I have tested.

Does not seem to reproduce on my current build: 10.0.16299 Build 16299 x64 (didnt have time to see if it's really fixed)

## last email response :)
Hey Marius,
   Your report requires either physical access or social engineering, and as such, does not meet the bar for servicing down-level (issuing a security patch).
   [...]
   
   Your attempt to responsibly disclose a potential security issue is appreciated and we hope you continue to do so.

Regards,

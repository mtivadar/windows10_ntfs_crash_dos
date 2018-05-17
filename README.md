# windows10_ntfs_crash_dos
PoC for a NTFS crash that I discovered, in various Windows versions

Type of issue: denial of service. One can generate blue-screen-of-death using a handcrafted NTFS
image. This Denial of Service type of attack, can be driven from user mode, limited user account or
Administrator. It can even crash the system if it is in locked state.

**Reported to Microsoft** on July 2017, they did not want to assign CVE for it nor even to write me when/if they will fix it.

To test, write the image: `dd.exe if=tinyntfs  of=\\.\<usb-drive-letter>: bs=1M count=10`
You can download dd from http://www.chrysocome.net/dd

Generally, with autoplay enabled, bsod will follow in seconds when usb stick is inserted. If this doesn't work, crash will occur when files get read. (Try accessing file named '4')

-~~Does not seem to reproduce on my current build: 10.0.16299 Build 16299 x64 (didnt have time to see if it's really fixed)~~

## Affected systems

| Name | Version | Release | Architecture| Compatibility | Tested by
| :--------------: | :--------------: | :--------------: | :--------------: | :--------------: | :--------------:
| Windows 7 Enterprise | 6.1.7601 SP1 | 7601 | x64 | :white_check_mark: | [@mtivadar](https://github.com/mtividar)
| Windows 7 Professional | 6.1.7601 SP1 | 7601 | x64 | :white_check_mark: | [@frankenstein91](https://github.com/frankenstein91)
| Windows 10 Professional | 10.0.15063 | 15063 | x64 | :white_check_mark: | [@mtivadar](https://github.com/mtividar)
| Windows 10 Professional | 10.0.16299 | 16299 | x64 | :white_check_mark: | [@mtivadar](https://github.com/mtividar)
| Windows 10 Professional | 10.0.16299.371 (WinBuild.160101.0800) | 1709 | x64 | :white_check_mark: |  [@wikijm](https://github.com/wikijm)
| Windows 10 Enterprise Evaluation Insider Preview | 10.0.16215 | 16215 | x64 | :white_check_mark: | [@mtivadar](https://github.com/mtividar)
| Microsoft Windows 10 Pro | 10.0.14393.206 (rs1_release.160915-0644) | 1607 | x64 | :white_check_mark: | [@mtivadar](https://github.com/mtividar)
| Microsoft Windows 10 Pro | 10.0.17134.1 (WinBuild.160101.0800) | 1803 | x64 | :white_check_mark: | [@mtivadar](https://github.com/mtividar)
| Microsoft Windows 8.1 Pro | 6.3.9600.17196 (winblue_gdr.140601-1505) | 9600 | x64 | :white_check_mark: | [@mtivadar](https://github.com/mtividar)
| Microsoft Windows XP | SP3 | - | x86 | :x: | [@mtivadar](https://github.com/mtividar)
| ReactOS | 0.4.8 | Build  20180405-0.4.8-release-0-gd47d448.GNU_4.7.2  | x86 | :x: | [@frankenstein91](https://github.com/frankenstein91)
|  |  |  |  | :grey_question: | [@akindgithubuser](https://github.com/akindgithubuser)


### How to get OS information (Powershell commands):
- Name:     ```Get-WmiObject -Class Win32_OperatingSystem | ForEach-Object -MemberName Caption ```
- Version:  ```(Get-ItemProperty -Path c:\windows\system32\hal.dll).VersionInfo.FileVersion```
- Release:  ```(Get-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion" -Name ReleaseId).ReleaseId```


Note: These are the only systems that have been tested, feel free to contribute through a pull request.


## last email response :)
Hey Marius,
   Your report requires either physical access or social engineering, and as such, does not meet the bar for servicing down-level (issuing a security patch).
   [...]

   Your attempt to responsibly disclose a potential security issue is appreciated and we hope you continue to do so.

Regards,


## LE
Fortunately, this bug can generate a BSOD and nothing more. It cannot be weaponized. Still, in some scenarios, a blue-screen-of-death could be unacceptable.

Microsoft was very responsive regarding my disclosure 1 year ago, but they didn’t issue a security patch.

In some cases it works by only inserting the memory stick, in other cases it works when a program tries to read files from that stick.

This bug apparently is not fixed yet, I can reproduce the crash on a latest Windows 10 build. Anyway, bug was reported almost 1 year ago.

As a security researcher, I think that every vulnerability that requires physical access and/or social engineering is important. I’ve seen and studied malware like FLAME, Stuxnet that may have been spread using physical access (FLAME and Stuxnet contained a 0-day exploit that forced the OS to run malware from a removable drive).
We all know the stories Kevin Mitnick taught us regarding social engineering, so yes, these types of bugs are important.

More than that, inserting a memory stick when a computer is in a locked state triggers the execution of a lot of OS code, such as mounting file systems. This could be dangerous if the file system is handcrafted and aimed at exploiting the OS. This behavior should be changed for any operating system.

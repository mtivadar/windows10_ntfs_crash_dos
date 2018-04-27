# windows10_ntfs_crash_dos
PoC for a NTFS crash that I discovered, in various Windows versions

Type of issue: denial of service. One can generate blue-screen-of-death using a handcrafted NTFS
image. This Denial of Service type of attack, can be driven from user mode, limited user account or Ad-
ministrator. It can even crash the system if it is in locked state.
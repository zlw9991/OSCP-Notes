# OSCP-Notes
Generic Notes Regarding OSCP:

1.[ Misc](#misc)

## Misc:

### Powershell Script Not Running
Sometimes, when .ps1 exploits do not work, it may be due to how the default powershell.exe used is incorrect.
In this case, try to use: C:\Windows\systenative\WindowsPowershell\v1.0\powershell.exe instead, this will call the x64 version of powershell which may be what is needed for kernel exploits since by default, the x86 powershell is run instead in  C:\Windows\System32\WindowsPowershell\v1.0\powershell.exe

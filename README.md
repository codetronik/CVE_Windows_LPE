# CVE-2024-49138

This repository was created based on the PoC at the following link.<p>
https://github.com/MrAle98/CVE-2024-49138-POC (2nd branch)

1. Download
* Windows 11 23H2 22621.2428
  * https://archive.org/download/win-11-23h2/Win11_23H2_English_x64.iso

* KB5046732
  * https://catalog.sf.dl.delivery.mp.microsoft.com/filestreamingservice/files/e082275c-9281-429a-be97-ac6fef637e92/public/windows11.0-kb5033375-x64_516f4fb2bb560cddf08e9d744de8029f802dec21.msu

* Vulnerable driver
  * https://msdl.microsoft.com/download/symbols/clfs.sys/DC7E0CA66f000/clfs.sys

2. Install Windows and cumulative updates

3. Replace clfs.sys
```
takeown /f C:\Windows\System32\drivers\clfs.sys
icacls C:\Windows\System32\drivers\clfs.sys /grant administrators:F
copy C:\Users\name\Downloads\clfs.sys C:\Windows\System32\drivers\clfs.sys
shutdown /r /t 0
```
4. Check your file hash
If the hash doesn’t match, it won’t work.
```
PS C:\Users\a> Get-FileHash c:\windows\system32\drivers\clfs.sys
Algorithm       Hash                                                                   Path
---------       ----                                                                   ----
SHA256          B138C28F72E8510F9612D07D5109D73065CED6CBBF8079A663A1E0601FE0FBAA       C:\windows\system32\drivers\clfs.sys
```
```
PS C:\> Get-FileHash c:\windows\system32\ntoskrnl.exe
Algorithm       Hash                                                                   Path
---------       ----                                                                   ----
SHA256          0CE15480462E9CD3F7CBF2D44D2E393CF5674EE1D69A3459ADFA0E913A7A2AEB       C:\windows\system32\ntoskrnl.exe
```

5. Run CVE-2024-49138.exe
No administrator privileges are required.

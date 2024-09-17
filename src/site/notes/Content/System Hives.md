---
{"dg-publish":true,"permalink":"/content/system-hives/","tags":["windows","forensics","hives"],"created":"2024-09-16T18:37:14.161-07:00","updated":"2024-09-16T18:43:18.282-07:00"}
---

## Overview
The 5 *root keys* are:
1. HKEY_CLASSES_ROOT (HKCR)
2. HKEY_USERS (HKU)
3. HKEY_CURRENT_USER (HKCU)
4. HKEY_LOCAL_MACHINE (HKLM)
5. HKEY_CURRENT_CONFIG (HKCC)
HKLM and HKU are the only root keys that Windows physically stores on files. HKCU is a symbolic link to subkey in HKU. HKCR and HKCC are symbolic links to subkeys in HKLM. 

HKLM is the most interesting, it also has 5 *registry keys*
1. HARDWARE
2. SAM (Security Accounts Manager)
3. SECURITY
4. SOFTWARE
5. SYSTEM

Subsequent levels are referred to as *subkeys*, which finally point to *values*. Most hives are located at `C:\Windows\System32\Config` but userhives are located at `C:\Users\<username>\`. A list of all *hive keys* is located at `HKLM\SYSTEM\CurrentControlSet\Control\hivelist`. The Windows registry can be viewed using `regedit`.

## HKEY_CLASSES_ROOT
running shell commands
- `.\exefile\shell\open\command`
- `.\batfile\shell\open\command`
- `.\comfile\shell\open\command`
- `.\Drive\shell` or `.\Drive\shell\cmd\command`
- `.\Folder\shell` or `.\Folder\shell\cmd\command`

## HKEY_CURRENT_USER

### HKCU\Software
MRU = Most Recently Used programs
- `.\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\OpenSaveMRU`
- `.\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\LastVisitedMRU`
- `.\Microsoft\Windows\CurrentVersion\Explorer\RunMRU`

`.\Microsoft\Internet Explorer\TypedURLs`
- corresponds to `%USERPROFILE%\Recent`
- shows links that are fully typed, autocompleted while typing, or selected from list of stored URLs in IE address bar
- **does not** show sites accessed via favourites or cleared history
- only records URLs after IE is closed

`.\Microsoft\Windows\CurrentVersion\Explorer\UserAssist`
- subkey starting with “5E6” is IE toolbar and “750” is Active Desktop
- registry values under these subkeys are ROT-13 encrypted

other notable entries
- `.\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs`
- `.\Microsoft\Windows\CurrentVersion\Explorer\Map Network Drive MRU`
- `.\Microsoft\Windows\CurrentVersion\Explorer\MountPoints2`
- `.\Microsoft\Protected Storage System Provider` (contains autocompleted logins)
- `.\Microsoft\Command Processor` has Autorun value that sets path of cmd.exe (check for modification)
- `.\Microsoft\Windows\CurrentVersion\Explorer\MountPoints2\CPC\Volume` shows mounted volumes that were assigned a drive letter
- `.\Microsoft\Search Assistant\ACMru` has terms used in Windows default search

## HKEY_LOCAL_MACHINE

### HKLM\SAM
SAM is a database that stores creds & user/group info
- backups at `C:\Windows\Repair\SAM` 
- get copy of hive: `reg.exe save hklm\sam C:\temp\sam.save`
- passwords are stored as either a LM or NT hash
	- null LM hash `aad3b435b51404eeaad3b435b51404ee` is empty
	- crack using secretsdumpy.py from Impacket or CrackMapExec

notable entries:
- `SAM\Domains\Account\Users`: last login date, password hint and password change dates of the users

### HKLM\Security
LSA (Local Security Authority) Secrets: LSA storage for creds
- located at `HKEY_LOCAL_MACHINE\Security\Policy\Secret`
- get copy of hive: `reg.exe save hklm\system C:\temp\system.save`

Decryption
- need Syskey from System hive to decrypt
- using impacket: `python3 secretsdump.py -security security.save -system system.save LOCAL`

### HKLM\Software
Programs store their settings in the standard form `HKLM\Software\Vendor\Program\Version`
- `.\Microsoft\Windows NT\CurrentVersion` contains OS info
- `.\Windows\Windows Portable Devices\Devices`
- `.\Microsoft\Windows\CurrentVersion\Run` has autorun entries that execute on startup
	- `.\Microsoft\Windows\CurrentVersion\RunOnce`
	- `.\Microsoft\Windows\CurrentVersion\RunOnceEx`
	- `.\Microsoft\Windows\CurrentVersion\RunServices`
	- `.\Microsoft\Windows\CurrentVersion\RunServicesOnce`
	- `.\Microsoft\Windows\CurrentVersion\Explorer\RunMRU`
- `.\Microsoft\Windows\CurrentVersion\Uninstall` shows installed programs that may not be in `Control Panel>Add/Remove Programs`
- `.\Microsoft\Windows NT\CurrentVersion\Image File Execution Options` lets you use any debugger with any program
- `.\Microsoft\Command Processor` has Autorun value that sets path of cmd.exe (check for modification)
- `.\Microsoft\Windows NT\CurrentVersion\Winlogon` has Shell value 
	- non-default value Taskman lets user run another task manager
- `.\Microsoft\WZCSVC\Parameters\Interfaces\GUID` shows wifi info

### HKLM\System
This hive contains Syskeys and has privledges
- get copy of hive: `reg.exe save hklm\system C:\temp\system.save`

notable entries:
- `.\CurrentControlSet\Control\Session Manager\AppCompatCache\AppCompatCache`
	- for compatability purposes, but can show evidence of execution (even if binary is deleted)
	- stored in memory, so it only updates on reboot
- `.\CurrentControlSet(or ControlSet)\Enum\USBSTOR`
- `.\MountedDevices'
- `.\CurrentControlSet\Services` contains list of Windows services
- `.\CurrentControlSet\Services\bam\UserSettings\{SID}` is the Background Activity Monitor (BAM) which runs on standby
- `.\CurrentControlSet\Services\dam\UserSettings\{SID}`, the Desktop Activity Moderator, is similar to BAM but optimizes power use
- `.\CurrentControlSet\Control\Session Manager\Memory Management` contains the virtual memory config
	- paging file usually at `C:\pagefile.sys`
	- can be deleted on shutdown by changing `ClearPagefileAtShutdown` value to 1
- `.\CurrentControlSet\Services\Tcpip\Parameters\Interfaces\GUID` has network adapter settings
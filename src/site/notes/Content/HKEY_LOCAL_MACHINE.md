---
{"dg-publish":true,"permalink":"/content/hkey-local-machine/","tags":["windows","forensics","hives"],"created":"2024-09-17T23:55:42.248-07:00","updated":"2024-09-18T00:00:02.589-07:00"}
---

---
HKLM is the most interesting *root key*, it also has 5 *registry keys*
1. HARDWARE (not important)
2. [[Content/HKEY_LOCAL_MACHINE#HKLM SAM\|SAM (Security Accounts Manager)]]
3. [[Content/HKEY_LOCAL_MACHINE#HKLM Security\|SECURITY]]
4. [[Content/HKEY_LOCAL_MACHINE#HKLM Software\|SOFTWARE]]
5. [[Content/HKEY_LOCAL_MACHINE#HKLM System\|SYSTEM]]
---
### HKLM\\SAM
SAM is a database that stores creds & user/group info
- backups at `C:\Windows\Repair\SAM` 
- get copy of hive: `reg.exe save hklm\sam C:\temp\sam.save`
- passwords are stored as either a LM or NT hash
	- null LM hash `aad3b435b51404eeaad3b435b51404ee` is empty
	- crack using secretsdumpy.py from Impacket or CrackMapExec

notable entries:
- `SAM\Domains\Account\Users`: last login date, password hint and password change dates of the users

### HKLM\\Security
LSA (Local Security Authority) Secrets: LSA storage for creds
- located at `HKEY_LOCAL_MACHINE\Security\Policy\Secret`
- get copy of hive: `reg.exe save hklm\system C:\temp\system.save`

Decryption
- need Syskey from System hive to decrypt
- using impacket: `python3 secretsdump.py -security security.save -system system.save LOCAL`

### HKLM\\Software
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

### HKLM\\System
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
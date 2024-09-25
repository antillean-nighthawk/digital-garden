---
{"dg-publish":true,"permalink":"/structure/windows/","tags":["windows","forensics"],"created":"2024-09-16T18:32:48.890-07:00","updated":"2024-09-17T23:45:38.375-07:00"}
---


- prefetch artifacts are located in `%Windows%\Prefetch`
- list of all Windows data structures: http://terminus.rewolf.pl/terminus/
- cut through Windows event logs using [chainsaw](https://github.com/WithSecureLabs/chainsaw)
# Windows-specific artifacts
## [[Content/AppCompat\|AppCompat]] ⭐ [[Structure/System Hives\|System Hives]] ⭐ [[Content/SRUM\|SRUM]]

## Stored Creds
- C:\unattend.xml
- C:\Windows\System32\
- C:\Windows\System32\sysprep\
- C:\sysprep.inf
- C:\sysprep\sysprep.xml
- C:\Windows\Panther\
- C:\Windows\Panther\Unattend\
### Parent/Child Relations
- all _svchost.exe_ processes should be a child of _services.exe_ 
	- anything else is malicious
- user processes are usually a child of _explorer.exe_
- some svchost.exe spawn office processes for Outlook preview
- parent of _cmd.exe_ is usually _explorer.exe_
	- parent should never be _iexplore.exe_ or _Acroread.exe_
#### PST files
use `pffexport` to view
- `pffexport` also shows personal folder files in MS Outlook
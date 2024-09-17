---
{"dg-publish":true,"permalink":"/structure/windows/","tags":["windows","forensics"],"created":"2024-09-16T18:32:48.890-07:00","updated":"2024-09-16T18:49:18.013-07:00"}
---


- prefetch artifacts are located in `%Windows%\Prefetch`
- list of all Windows data structures: http://terminus.rewolf.pl/terminus/
- cut through Windows event logs using [chainsaw](https://github.com/WithSecureLabs/chainsaw)

## [[Content/AppCompat\|AppCompat]]
## [[Content/System Hives\|System Hives]]

## Stored Creds
- C:\unattend.xml
- C:\Windows\System32\
- C:\Windows\System32\sysprep\
- C:\sysprep.inf
- C:\sysprep\sysprep.xml
- C:\Windows\Panther\
- C:\Windows\Panther\Unattend\

### Parent/Child
- all _svchost.exe_ processes should be a child of _services.exe_ 
	- anything else is malicious
- user processes are usually a child of _explorer.exe_
- some svchost.exe spawn office processes for Outlook preview
- parent of _cmd.exe_ is usually _explorer.exe_
	- parent should never be _iexplore.exe_ or _Acroread.exe_

## SRUM
The System Resource Utilization Monitor (SRUM) has hourly captures of network and app usage that span the past 1-2 months. It is located at `%SYSTEM%\SRU\SRUDB.DAT` but it's good to get the whole _SRU_ folder since there might be unsynced entries in the _.log_ files.

Useful info:
1. Names and paths of executed apps
2. User SID of account that executed the app
3. Networks the system connected to
4. App resource usage (CPU cycles, I/O bytes, etc)
5. Network data usage (bytes sent/received per app)

SRUM to Excel converter: https://github.com/MarkBaggett/srum-dump

#### PST files
use `pffexport` to view
- `pffexport` also shows personal folder files in MS Outlook
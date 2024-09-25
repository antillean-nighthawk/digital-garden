---
{"dg-publish":true,"permalink":"/content/app-compat/","tags":["windows","apps","forensics"],"created":"2024-09-16T18:35:52.384-07:00","updated":"2024-09-16T18:43:39.200-07:00"}
---


A directory that contains info about applications on the system.

## PCA
The PCA (Program Compatibility Assistant) directory is located at `C:\Windows\AppCompat\PCA`. It contains several text files that track application status.

- PcaGeneralDb0.txt
	- various app runtime details
- PcaGeneralDb1.txt
	- shows apps that exited with an error + has everything in _PcaGeneralDb0.txt_
- PcaAppLaunchDic.txt
	- app file paths and most recent execution timestamp

## Amcache
This hive has a special directory path `C:\Windows\AppCompat\Programs\AmCache.hve`. It shows details of recently executed apps, which are pulled from the _Amcache.hve.LOG#_ files. The last write time of the registry key is the first instance of app execution. It also shows a SHA1 hash but this is only calculated using the first 30MB of the binary so be wary of collisions.
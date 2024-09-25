---
{"dg-publish":true,"permalink":"/content/hkey-current-user/","tags":["windows","forensics","hives"],"created":"2024-09-17T23:51:02.591-07:00","updated":"2024-09-17T23:55:24.653-07:00"}
---

## HKCU\\Software
### MRU
MRU = Most Recently Used programs
- `.\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\OpenSaveMRU`
- `.\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\LastVisitedMRU`
- `.\Microsoft\Windows\CurrentVersion\Explorer\RunMRU`
### TypedURLs
`.\Microsoft\Internet Explorer\TypedURLs`
- corresponds to `%USERPROFILE%\Recent`
- shows links that are fully typed, autocompleted while typing, or selected from list of stored URLs in IE address bar
- **does not** show sites accessed via favourites or cleared history
- only records URLs after IE is closed
### UserAssist
`.\Microsoft\Windows\CurrentVersion\Explorer\UserAssist`
- subkey starting with “5E6” is IE toolbar and “750” is Active Desktop
- registry values under these subkeys are ROT-13 encrypted
### Explorer
- `.\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs`
- `.\Microsoft\Windows\CurrentVersion\Explorer\Map Network Drive MRU`
- `.\Microsoft\Windows\CurrentVersion\Explorer\MountPoints2`
- `.\Microsoft\Windows\CurrentVersion\Explorer\MountPoints2\CPC\Volume`
	- shows mounted volumes that were assigned a drive letter
### Other notable entries
- `.\Microsoft\Protected Storage System Provider` (contains autocompleted logins)
- `.\Microsoft\Command Processor` has Autorun value that sets path of cmd.exe (check for modification)
- `.\Microsoft\Search Assistant\ACMru` has terms used in Windows default search
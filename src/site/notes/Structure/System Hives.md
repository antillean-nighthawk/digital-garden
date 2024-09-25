---
{"dg-publish":true,"permalink":"/structure/system-hives/","tags":["windows","forensics","hives"],"created":"2024-09-16T18:37:14.161-07:00","updated":"2024-09-18T00:01:26.102-07:00"}
---

The 5 *root keys* are:
1. [[Content/HKEY_CLASSES_ROOT\|HKEY_CLASSES_ROOT (HKCR)]]
2. HKEY_USERS (HKU)
3. [[Content/HKEY_CURRENT_USER\|HKEY_CURRENT_USER (HKCU)]]
4. [[Content/HKEY_LOCAL_MACHINE\|HKEY_LOCAL_MACHINE (HKLM)]]
5. HKEY_CURRENT_CONFIG (HKCC)

> HKLM and HKU are the only root keys that Windows physically stores on files. HKCU is a symbolic link to subkey in HKU. HKCR and HKCC are symbolic links to subkeys in HKLM. 

Subsequent levels are referred to as *subkeys*, which finally point to *values*. Most hives are located at `C:\Windows\System32\Config` but user hives are located at `C:\Users\<username>\`. A list of all *hive keys* is located at `HKLM\SYSTEM\CurrentControlSet\Control\hivelist`. The Windows registry can be viewed using `regedit`.
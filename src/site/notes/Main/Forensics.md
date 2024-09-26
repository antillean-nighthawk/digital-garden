---
{"dg-publish":true,"permalink":"/main/forensics/","tags":["forensics"]}
---


#### Topics by OS: [[Structure/Windows\|Windows]]
#### Topics by [[Structure/Files\|filetype]]

---

- check artifacts such as memdumps and log files
- verify checksum has not changed
	- generate hashes using `md5sum`, `sha256sum`, etc
- use [AccessData FTK Imager](http://accessdata.com/product-download) to capture disk images
- use write blocker _before_ imaging disk to maintain integrity
- [PhotoRec](https://www.cgsecurity.org/wiki/PhotoRec) works with broken filesystems
- Autopsy GUI or Volatility for analysis
- [mount disk images in vm](https://habr.com/en/articles/444940/)
- `evtxtract` carves event log xml fragments
- other data carving tools: `page_brute`, `yara`, `yarp suite`, `bulk extractor`
- [FLOSS](https://github.com/mandiant/flare-floss) auto-extract obfuscated strings from malware

## Volatility
determine the OS and set as profile before using modules

https://ctf101.org/forensics/what-is-memory-forensics/

plugins for SQL, browser history, network packets, and more

Volatility CLI is `volshell`

Volatility GUI here: https://github.com/memoryforensics1/Vol3xp

### Memory Analysis Workflow
1. Run strings for clues
2. Identify the image profile (which OS, version, etc.)
3. Dump processes and look for suspicious processes
4. Dump data related interesting processes
5. View data in a format relating to the process (Word: .docx, Notepad: .txt, Photoshop: .psd, etc.)

## Processes

### Carving
Process structures can be carved like other files. For example, Volatility's `windows.psscan` carves blocks based on the *_EPROCESS* tag. Recovered process structures might not point to valid virtual addresses if they are overwritten, which will result in an error when trying to dump it.

> [!WARNING] Zombies
Zombies are terminated processes that are still in process list, usually because the parent is still alive. Has 0 threads and an exit time.

### Warning Signs
- look-alike names
- usual duplicates of singleton processes
- process running from non-default path
- suspicious CLI params
- unusual PID relationships
- unexpected behaviour from a process

## More Tools
- https://forensics.wiki/tools/
- https://fareedfauzi.github.io/2023/12/22/Windows-Forensics-checklist-cheatsheet.html
- https://fareedfauzi.github.io/2024/03/29/Linux-Forensics-cheatsheet.html
---
{"dg-publish":true,"permalink":"/content/general/","tags":["ctf","general"],"created":"2024-09-16T18:25:59.303-07:00","updated":"2024-09-16T19:28:28.378-07:00"}
---

anything not enough to warrant its own category goes here

- `exiftool` metadata
- use `strings` and `grep -i` for flag
	- `quantumstrands` is a more advanced alternative to `strings`
- check hash to see if file has been modified
- read ELF binaries: `readelf -h /bin/ping`
- buffer overflow: `python -c 'print "A"*30' | ./bad`
- password cracking: use `hashcat` or `john the ripper`
- check the [timeline](https://ctf101.org/forensics/what-is-metadata/) of a file
- [CNC Gcode viewer](https://ncviewer.com/)
- run binary as different architecture using `linux64 ./<binary>` or `linux32 ./<binary>`
- [CTFtime](https://ctftime.org/) lists all upcoming CTFs

## Scripting and programming
- [Dockerfile linter](https://hadolint.github.io/hadolint/)
- [Bash commands tldr](https://tldr.inbrowser.app/)
- [Shell script linter](https://www.shellcheck.net/)
- [Explain CLI commands](https://explainshell.com/)
- [Search website source code](https://publicwww.com/)
- [Advanced awk/sed usage](https://posts.specterops.io/fawk-yeah-advanced-sed-and-awk-usage-parsing-for-pentesters-3-e5727e11a8ad)
---
{"dg-publish":true,"permalink":"/content/zip/","tags":["file","zip","forensics"],"created":"2024-09-16T19:06:47.067-07:00","updated":"2024-09-16T19:08:08.635-07:00"}
---

### 7zip, zip, zipx
once unzipped, go back to [[Structure/Files\|Files]]
## Info
- `zipdetails -v` shows values of format fields
- `zipinfo` shows info about contents w/o unzipping
## Corruption
- `unzip` shows info on why a zip will not decompress
- `zip -F input.zip --out output.zip` and `zip -FF input.zip --out output.zip` try to repair corrupted files
## Passwords
- `fcrackzip` brute-forces passwords that are ~<7 chars
- password-protected zip files don't encrypt the filenames and original file sizes of the compressed files they contain, unlike password-protected RAR or 7z files
- [zip plaintext attack](https://wiki.anter.dev/misc/plaintext-attack-zipcrypto/#prerequisites) for older ZipCrypto format (not AES-256)
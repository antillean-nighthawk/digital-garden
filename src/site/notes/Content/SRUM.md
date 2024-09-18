---
{"dg-publish":true,"permalink":"/content/srum/","tags":["forensics","windows"],"created":"2024-09-17T23:41:52.243-07:00","updated":"2024-09-17T23:43:01.666-07:00"}
---

The *System Resource Utilization Monitor (SRUM)* has hourly captures of network and app usage that span the past 1-2 months. It is located at `%SYSTEM%\SRU\SRUDB.DAT` but it's good to get the whole _SRU_ folder since there might be unsynced entries in the _.log_ files.
### Useful info
1. Names and paths of executed apps
2. User SID of account that executed the app
3. Networks the system connected to
4. App resource usage (CPU cycles, I/O bytes, etc)
5. Network data usage (bytes sent/received per app)

SRUM to Excel converter: https://github.com/MarkBaggett/srum-dump
---
{"dg-publish":true,"permalink":"/content/email/","tags":["forensics","email","file"],"created":"2024-09-16T18:53:22.961-07:00","updated":"2024-09-16T19:02:20.430-07:00"}
---


### eml, msg
---
valid DKIM = you have the same email that was sent/received
valid ARC = you have the same email that was received, which may not necessarily be the same which was sent

---
.MSG files are OLE files, refer to [[Content/Microsoft Office\|Microsoft Office]] section

---
if the email contains an .ics calendar invite, it needs base64 decoding to be viewable

---
> [!FAQ]- How to get DKIM hash
> 1. look up [d-value]:[s-value] to get public key
> 2. include all fields in [h-value] (including dupes and empty fields) in order, followed by [bh-value]
> 	1. can also calculate body hash yourself (between and including MIME boundaries and CRLF)
> 3. calculate DKIM hash using algorithm specified in [a-value]
> 
> [DKIM specification](https://datatracker.ietf.org/doc/html/rfc6376)

> [!DANGER] Modification
Users can set the _From_ header to anything and doesn't necessarily have to match the _Return-Path_. _Authentication-Results_, _Received-SPF_, almost anything in an email can be forged.

Check for tampering:
- check DKIM hash 
- differences in HTML and text sections
- inconsistent timestamps or timezones
- visual misalignment
	- for example, if `Content-Transfer-Encoding: quoted-printable` then the line should be <77 chars
- duplicate Message-ID or in a format inconsistent with the server it is sent from
- implausible X-Mailer user-agent
- timestamp ending in all 0s with exact granularity
- missing header fields (particularly those starting with X)
## Hidden timestamps
There can be present in various email fields and formats. 
- MIME boundary delimiters
- Message-ID
- References or In-Reply-To
- DKIM-Signature (sometimes)
- Received or X-Received
- Authentication-Results
- Content-Type
- Thread-Index

```python
# decode Gmail MIME boundary
# from https://thinkdfir.com/2021/02/09/metaspike-ctf-week-6-hodl-onto-your-timestamps/
from datetime import datetime

boundary = "000000000000ee186a05b959a8f0" # for example

ts = int(boundary[18:-2] + boundary[12:-10], 16) / 1000000
print(datetime.utcfromtimestamp(ts).strftime('%Y-%m-%d %H:%M:%S') + " UTC")
```

More details in Metaspike's _Dates in Hiding_ series:
1. https://www.metaspike.com/timestamps-forensic-email-examination/
2. https://www.metaspike.com/gmail-mime-boundary-delimiter-timestamps/
3. https://www.metaspike.com/dates-gmail-message-id-thread-id-timestamps/

## Phishing
warning signs:
- original Received header or Return-Path is implausible
- no SPF enforced
- no DKIM either
- suspicious X-Originating-IP or X-Originating-Org
## Tools
https://mha.azurewebsites.net/ - Microsoft email header viewer
https://analyzer.sublime.security/ - Sublime's email sandbox
https://mxtoolbox.com/ - swiss army knife for email analysis
https://www.digital-detective.net/dcode/ - timestamp decoding utility
https://digitalsleuth.gitbook.io/time-decode-documentation - Python timestamp library
https://www.meridiandiscovery.com/how-to/e-mail-conversation-index-metadata-computer-forensics/ - thread index parser
---
{"dg-publish":true,"permalink":"/content/microsoft-office/","tags":["microsoft","office","forensics","file"],"created":"2024-09-16T19:01:21.851-07:00","updated":"2024-09-18T23:52:41.141-07:00"}
---

### doc, ppt, xml

> https://attack.mitre.org/techniques/T1137/
> MS Office files can distribute phishing or malware via _macros_ (VBA scripts). A typical VBA macro in an Office document attempts to download a PowerShell script to %TEMP% and execute it. 
## MS filetypes
1. OLE/OLE2 (Object Linking and Embedding)
	- file extensions like RTF, DOC, XLS, PPT
	- can contain macros
	- have a signature of `DOCFILE`
1. OOXML (Office Open XML)
	- replaced OLE format in Office 2007
	- file extensions that include DOCX, XLSX, PPTX
	- these are actually _zip_ containers that can be unzipped
	- don't contain macros, but can contain OLEs
3. RTF (Rich Text Format)
	- lets you open Office files in other (non-MS) applications
	- don't contain macros but can have embedded files/objects
## Analysis
- similar to [[PDF\|PDF]] analysis
- `oletools` or `officedissector` Python library
	- or [`oledump.py`](https://github.com/DidierStevens/DidierStevensSuite/blob/master/oledump.py)
- [VBA extractor](https://www.onlinehashcrack.com/tools-online-extract-vba-from-office-word-excel.php)
- execute macro from CLI
	- `$ soffice path/to/test.docx macro://./standard.module1.mymacro`
- debug complex macros using Office apps or LibreOffice (FOSS!)
- submit a malicious file to [Microsoft](https://www.microsoft.com/en-us/wdsi/filesubmission) for review
- [MalDocA](https://github.com/google/maldoca)
## Guides
- https://zeltser.com/analyzing-malicious-documents/
- https://amgedwageh.medium.com/pillars-of-analyzing-malicious-ms-office-documents-part-1-3-document-format-structures-89d5c73be66
---
{"dg-publish":true,"permalink":"/content/image/","tags":["image","forensics","ctf","file"],"created":"2024-09-16T18:59:12.536-07:00","updated":"2024-09-16T19:02:35.648-07:00"}
---


### png, jpg, jpeg

Python libraries: `qrtools`, `pillow`
## Metadata
- view metadata using `exiftool <filename>`
- view/edit magic numbers using [hexedit](https://hexed.it/)
- can also get hexdump from `xxd`
## Image Carving
- find and extract hidden files using `binwalk`, `foremost`, or `steghide`
- stegano-hidden data: `zsteg -a <filename.png>`
- use `tesseract` to convert text in image to .txt file
- `stegcracker` for passphrase
- `stegoveritas` for LSB extraction
- other tools: `stegdetect`, `stegsolve`, `crypture`, `rsteg`, `openstego`, `jsteg`
- could also do it manually using `dd`, but why would you do that

## Cropped
Acropalypse vuln: just sticks a IEND chunk in the middle 💀

https://acropalypse.app/

https://github.com/frankthetank-music/Acropalypse-Multi-Tool/

## Fix broken .pngs
- [crc32fix](https://github.com/Aloxaf/crc32fix): fix height/width based on checksum
- [PCRT](https://github.com/sherlly/PCRT): fix header/footer
- [png-crc-fix](https://github.com/landaire/png-crc-fix): fix checksum
- [pngcheck](http://www.libpng.org/pub/png/apps/pngcheck.html): look for errors

## Visual Edits
- try zooming in or out a lot (~200-300% to avoid false positives)
- scale, shadow or perspective errors indicate Photoshop
- airbrushing, shine or repeating patterns indicate AI generated
- change brightness, saturation, opacity etc
- reverse image search: [Yandex](https://yandex.com/images/), [Tineye](https://tineye.com/), [Google](https://images.google.com/)
- use Gimp or ImageMagick
- depixelate text with [Depix](https://github.com/spipm/Depix)
- facial recognition: https://facecheck.id/

> Ruby script to highlight colors: https://pastebin.com/46VmzrRU

## Helpful Sites
- https://aperisolve.com/ 
- https://georgeom.net/StegOnline/
- https://stylesuxx.github.io/steganography/
- https://futureboy.us/stegano/decinput.html
- https://magiceye.ecksdee.co.uk/
- https://29a.ch/photo-forensics/
- https://online.officerecovery.com/pixrecovery/
- https://www.photopea.com/
- https://fotoforensics.com/
- https://www.imageforensic.org/
---
{"dg-publish":true,"permalink":"/content/video/","tags":["file","video","forensics","ctf"],"created":"2024-09-16T19:05:15.127-07:00","updated":"2024-09-16T19:06:29.353-07:00"}
---

### mkv, mp4, gif

video files are just _container_ formats that multiplex audio and video 

use `ffmpeg` to analyze video (`ffmpy` in Python)
- get info: `ffmpeg -i chal.mkv`
- subtitle: `ffmpeg -i chal.mkv -map 0:s:0 subs.srt`
- fonts: `ffmpeg -dump_attachment:t "" -i chal.mkv`

look at gifs frame by frame and analyze the same way as [[Content/Image\|images]]
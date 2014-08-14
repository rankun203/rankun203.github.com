---
layout: post
title: "Using FFmpeg to do some simple video process."
date: 2014-04-26 21:23:05 +0800
comments: true
categories: ["ffmpeg"]
---

Tip:

> zsh doesn't support letters like '[', ']' etc. so we need to add a Back Slash(\\)

> rake new\_post\\["kicking the ffmpeg"\\]

###Because

FFmpeg can't concatenate .mp4 videos directly, but .ts is ok. 

###So

We need to convert all .mp4 files to .ts, then concatenate them together.

####Convert

```bash
ffmpeg -i 1.mp4 -c:v copy -c:a copy -vbsf h264_mp4toannexb 1.ts
ffmpeg -i 2.mp4 -c:v copy -c:a copy -vbsf h264_mp4toannexb 2.ts
...
```

1. `-c:a copy` to tell FFmpeg to copy the audio stream, `-c:v copy` has the same mean.
2. `-vbsf h264_mp4toannexb` a encoder use to convert videos to .ts.
3. `-i` input file

####Concatenate

```bash
ffmpeg -i "concat:1.ts|2.ts|3.ts|4.ts" -c:v copy -c:a copy -absf aac_adtstoasc output.mp4
```

###To simplify this, we need a script as a little program.

```bash
#Not implement yet
```

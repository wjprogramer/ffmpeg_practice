# FFmpeg

## CH1

p4

```
set INPUT=cc0_videos/sample_360.mp4
set OUTPUT=output/p4.mp4
ffmpeg -i %INPUT% -vf "split [main][tmp]; [tmp] crop=iw:ih/2:0:0, vflip [flip]; [main][flip] overlay=0:H/2" %OUTPUT%
```

p6

```
set INPUT=cc0_videos/sample_360.mp4
set OUTPUT=output/p6.avi
ffmpeg -i %INPUT% %OUTPUT%
```

p7

```
set INPUT=cc0_videos/sample_360.mp4
set OUTPUT=output/p7.dat
ffmpeg -i %INPUT% -f avi %OUTPUT%
```

p10

```
set INPUT=cc0_videos/sample_360.mp4
ffprobe -show_streams %INPUT%
```

## CH2

p30

```
ffmpeg --help
```

p31

```
ffmpeg --help long
```

```
ffmpeg --help full
```

p39

```
set INPUT=cc0_videos/sample_360.mp4
set OUTPUT=output/p39.mp4
ffmpeg -i %INPUT% -vcodec mpeg4 -b:v 200k -r 15 -an %OUTPUT%
```

p41

```
set INPUT=cc0_videos/sample_360.mp4
ffprobe -show_packets %INPUT%
```

p52

```
set INPUT=cc0_videos/sample_360.mp4
ffplay -ss 30 -t 10 %INPUT%
```

```
set INPUT=cc0_videos/sample_360.mp4
ffplay -window_title "My Test" -t 10 %INPUT%
```

p53

```
set INPUT=rtmp://
ffplay -window_title "串流測試" %INPUT%
```

p56

```
set INPUT=cc0_videos/sample_360.mp4
ffplay -window_title "串流測試" -vf "subtitles=subtitles/subtitle.srt" %INPUT%
```

p57

```
set INPUT=cc0_videos/sample_360.mp4
ffplay -showmode 1 %INPUT%
```

```
set INPUT=cc0_videos/sample_360.mp4
ffplay -debug vis_mb_type -window_title "show vis_mb_type" -ss 20 -t 10 -autoexit %INPUT%
```

p58

```
set INPUT=cc0_videos/sample_360.mp4
ffplay -vismv pf %INPUT%
```

## CH3

p79

```
ffmpeg -h demuxer=mp4
```

p96

```
set INPUT=cc0_videos/sample_360.mp4
set OUTPUT=output/p96.m3u8
ffmpeg -re -i %INPUT% -c copy -f hls -bsf:v h264_mp4toannexb %OUTPUT%
```

## CH4

p

```
```

p

```
```

p

```
```

## CH6

p183

```
set INPUT=cc0_videos/sample_360.mp4
set LOGO=logo.png
set OUTPUT=output/p183.mp4
ffmpeg -i %INPUT% -i %LOGO% -filter_complex "[1:v]scale=1000:904[logo];[0:v][logo]overlay=x=0:y=0" %OUTPUT%
```

p184

```
set INPUT=cc0_videos/sample_360.mp4
set OUTPUT=output/p184.mp4
ffmpeg -i %INPUT% -vf "drawtext=fontsize=100:fontfile=FreeSerif.ttf:text='Hello World':x=20:y=70" %OUTPUT%
```

p192

```
set INPUT=cc0_videos/sample_360.mp4
set OUTPUT=output/p192.mp4
ffmpeg -re -i %INPUT% -re -i %INPUT% -re -i %INPUT% -re -i %INPUT% -filter_complex "nullsrc=size=640x480 [base]; [0:v] setpts=PTS-STARTPTS, scale=320x240 [upperleft]; [1:v] setpts=PTS-STARTPTS, scale=320x240 [upperright]; [2:v] setpts=PTS-STARTPTS, scale=320x240 [lowerleft]; [3:v] setpts=PTS-STARTPTS, scale=320x240 [lowerright]; [base][upperleft] overlay=shortest=1 [tmp1]; [tmp1][upperright] overlay=shortest=1:x=320 [tmp2]; [tmp2][lowerleft] overlay=shortest=1:y=240 [tmp3]; [tmp3][lowerright] overlay=shortest=1:x=320:y=240" -c:v libx264 %OUTPUT%
```

- -re (input): Read input at native frame rate. Mainly used to simulate a grab device, or live input stream (e.g. when reading from a file). Should not be used with actual grab devices or live input streams (where it can cause packet loss). By default ffmpeg attempts to read the input(s) as fast as possible. This option will slow down the reading of the input(s) to the native frame rate of the input(s). It is useful for real-time output (e.g. live streaming). 

p

```
```

p

```
```

p

```
```

p

```
```

p

```
```

p

```
```

p

```
```

p

```
```

p

```
```

p

```
```

p

```
```


## Practice

```
set INPUT=rtsp://admin:winsonic16350755@59.120.179.81:5540/chID=1&streamType=sub&linkType=tcp
ffplay -rtsp_transport tcp  "%INPUT%"
```

[ref](https://superuser.com/questions/1410764/how-to-play-two-remote-streams-simultaneously)

```
ffmpeg -headers X -i .. -headers Y -i .. -c copy -f nut - | ffplay -f nut -i -

# 練習
set INPUT=rtsp://admin:winsonic16350755@59.120.179.81:5540/chID=1&streamType=sub&linkType=tcp
ffmpeg \
-re -headers -i -rtsp_transport tcp %INPUT% \
-re -headers -i -rtsp_transport tcp %INPUT% \
-re -headers -i -rtsp_transport tcp %INPUT% \
-re -headers -i -rtsp_transport tcp %INPUT% \
-filter_complex "nullsrc=size=640x480 [base]; [0:v] setpts=PTS-STARTPTS, scale=320x240 [upperleft]; [1:v] setpts=PTS-STARTPTS, scale=320x240 [upperright]; [2:v] setpts=PTS-STARTPTS, scale=320x240 [lowerleft]; [3:v] setpts=PTS-STARTPTS, scale=320x240 [lowerright]; [base][upperleft] overlay=shortest=1 [tmp1]; [tmp1][upperright] overlay=shortest=1:x=320 [tmp2]; [tmp2][lowerleft] overlay=shortest=1:y=240 [tmp3]; [tmp3][lowerright] overlay=shortest=1:x=320:y=240" -c:v libx264 -c copy -f nut - | ffplay -f nut -i -
```

[ref](https://stackoverflow.com/questions/33662523/how-to-pipe-the-ffmpeg-output-to-multiple-ffplay)

```
set INPUT="rtsp://admin:winsonic16350755@59.120.179.81:5540/chID=1&streamType=sub&linkType=tcp"
ffmpeg -re -rtsp_transport tcp -i %INPUT% -f mpegts udp://224.0.0.1:10000
ffplay udp://224.0.0.1:10000
```


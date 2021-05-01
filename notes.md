# FFmpeg

## CH1

p4

```
set INPUT=sample_360.mp4
set OUTPUT=output/p4.mp4
ffmpeg -i %INPUT% -vf "split [main][tmp]; [tmp] crop=iw:ih/2:0:0, vflip [flip]; [main][flip] overlay=0:H/2" %OUTPUT%
```

p6

```
set INPUT=sample_360.mp4
set OUTPUT=output/p6.avi
ffmpeg -i %INPUT% %OUTPUT%
```

p7

```
set INPUT=sample_360.mp4
set OUTPUT=output/p7.dat
ffmpeg -i %INPUT% -f avi %OUTPUT%
```




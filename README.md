# Dash-Encoder
This repo shows you how to convert a .mp4 file to bitstreams and manifest.mpd file so that you can implement adaptive streaming. No need to pay microsoft azure for their media servers You can implement your own adaptive streaming server which will play the video according to the clients bandwidth 

### First you need to install ffmpeg on your server or local machine
[Download ffmpeg](https://ffmpeg.org/download.html)

## Setup <br />
```cmd
mkdir dash
```
>insert a input.mp4 file in folder dash

## Encode Video

> Encode to 360p Quality
```cmd
ffmpeg -i input.mp4 -c:v libvpx-vp9 -keyint_min 150 -g 150 -tile-columns 4 -frame-parallel 1 -f webm -dash 1 -an -vf scale=160:90 -b:v 250k -dash 1 video_160x90_250k.webm  
```
> Encode to 480p Quality
```cmd
ffmpeg -i input.mp4 -c:v libvpx-vp9 -keyint_min 150 -g 150 -tile-columns 4 -frame-parallel 1  -f webm -dash 1 -an -vf scale=320:180 -b:v 500k -dash 1 video_320x180_500k.webm
```

> Encode to 720p Quality
```cmd
ffmpeg -i input.mp4 -c:v libvpx-vp9 -keyint_min 150 -g 150 -tile-columns 4 -frame-parallel 1  -f webm -dash 1 -an -vf scale=640:360 -b:v 750k -dash 1 video_640x360_750k.webm
```
> Create manifest.mpd file
```cmd
ffmpeg -f webm_dash_manifest -i video_160x90_250k.webm  -f webm_dash_manifest -i video_320x180_500k.webm -f webm_dash_manifest -i video_640x360_750k.webm -f webm_dash_manifest -i my_audio.webm -c copy -map 0 -map 1 -map 2 -map 3 -map 4 -f webm_dash_manifest -adaptation_sets "id=0,streams=0,1,2,3 id=1,streams=4" manifest.mpd
```

## To know more about dash implement visit the [Link](https://github.com/Vishnu-yes-i-am/dash-player) .You will get the implemented dash code for both server and client .
### Please dont forget to Star Repo if it helped You .
Thank You



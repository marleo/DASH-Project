# DASH-Project
Video project for a master's course in AAU.

# Encoding
BigBuckBunny sample video was downloaded in 4k 30fps. Afterwards, it was encoded into 720p 2.5k bitrate, 480p 1k bitrate and 360p 0.5k bitrate like follows:
```
ffmpeg -i Big_Buck_Bunny_4k.mp4 -c:v libx264 -b:v 2500k -vf "scale=1280:720" -preset fast -c:a aac -b:a 128k Big_Buck_Bunny_720p.mp4
ffmpeg -i Big_Buck_Bunny_4k.mp4 -c:v libx264 -b:v 1000k -vf "scale=854:480" -preset fast -c:a aac -b:a 128k Big_Buck_Bunny_480p.mp4
ffmpeg -i Big_Buck_Bunny_4k.mp4 -c:v libx264 -b:v 500k -vf "scale=640:360" -preset fast -c:a aac -b:a 128k Big_Buck_Bunny_360p.mp4
```

These 3 videos were then packaged with MP4Box to DASH:
```
MP4Box -dash 4000 -frag 4000 -rap -segment-name segment_%s -url-template -out manifest.mpd Big_Buck_Bunny_720p.mp4#video:id=vid1:name=720p Big_Buck_Bunny_480p.mp4#video:id=vid2:name=480p Big_Buck_Bunny_360p.mp4#video:id=vid3:name=360p
```

The segments and the respective mpd file were then hosted via GitHub pages.

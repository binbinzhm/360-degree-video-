# step1

original.mp4 >> original.yuv

`ffmpeg -i original.mp4 original.yuv` 

# step2

original.yuv >> video-16Mb.hvc
original.yuv >> video-32Mb.hvc
original.yuv >> video-64Mb.hvc

`kvazaar -i original.yuv --input-res 76800x3840 -o video-16Mb.hvc --tiles 3x3 --slices tiles --mv-constraint frametilemargin --bitrate 16000000`

# step3

video-16Mb.hvc >> video-16Mb.mp4
video-32Mb.hvc >> video-32Mb.mp4
video-64Mb.hvc >> video-64Mb.mp4

`MP4Box -add video-16Mb.hvc:split_tiles -new video-16Mb.mp4`

# step4

video-16Mb.mp4 + video-32Mb.mp4 + video-64Mb.mp4 >> video16-32-64/*

`MP4box -dash 1000 -rap -frag-rap -profile live -out video16-32-64Mb.mpd video-16Mb.mp4 video-32Mb.mp4 video-64Mb.mp4` 




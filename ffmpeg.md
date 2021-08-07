# ffmeg tricks

## Convert to audio
    ffmpeg -i input.mp4 -vn -ar 44100 -ac 2 -b:a 96k output.mp3

## Record screen
    ffmpeg -f x11grab -s 19200x1080 -i :0.0 output.mkv

## Record from webcam
    ffmpeg -i /dev/video0 output.mkv


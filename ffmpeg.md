# ffmeg tricks

## Convert to audio
    ffmpeg -i input.mp4 -vn -ar 44100 -ac 2 -b:a 96k output.mp3

## Record screen
    ffmpeg -f x11grab -s 19200x1080 -i :0.0 output.mkv

## Record from webcam
    ffmpeg -i /dev/video0 output.mkv

## Convert MTS files into MP4
    IFS=$(echo -en "\n\b"); for i in *.MTS; do ffmpeg -i "$i" -c:a aac -strict experimental -b:a 128k "$i.mp4"; done

## Convert MP4 files into Youtube ready MP4
    ffmpeg -i input.mp4 -c:v libx264 -c:a aac -strict experimental -b:a 192k output.mp4
    for i in *.mp4; do ffmpeg -i "$i" -c:v libx264 -c:a aac -strict experimental -b:a 192k "new_$i"; done

    for i in *.mp4; do ffmpeg -i "$i" -c:v libx264 -c:a aac -strict experimental -b:a 192k "new_$i"; done

## Lower video size
	ffmpeg -i <path_to_video_file> -vcodec libx265 -crf 28 convertedVideo.mp4

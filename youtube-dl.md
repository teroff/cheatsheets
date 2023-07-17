# youtube-dl commands & tricks

## Download video from Youtube and replace the name with the video title
	yt-dlp --output '%(title)s.%(ext)s' '<link-to-youtube-video>'

## Download a playlist from Youtube and replace the names with the video titles
	yt-dlp -i -f mp4 --output '%(title)s.%(ext)s' --yes-playlist '<link-to-youtube-playlist>'
	yt-dlp -f mp4 --output '%(title)s.%(ext)s' -i <playlist-id>

## Download from a file with link and replace the names with the video titles
	yt-dlp --output '%(title)s.%(ext)s' -a <filename>

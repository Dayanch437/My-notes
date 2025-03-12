

git config --global url."git@github.com:".insteadOf "https://github.com/"



To join an audio and video file using FFmpeg, you can use the following command:


ffmpeg -i video.mp4 -i audio.mp3 -c:v copy -c:a aac -strict experimental output.mp4


Explanation:

- `-i video.mp4`: Input video file.
- `-i audio.mp3`: Input audio file.
- `-c:v copy`: Copy the video stream without re-encoding.
- `-c:a aac`: Encode the audio to AAC format (you can adjust if needed).
- `-strict experimental`: Enables experimental features for audio encoding.
- `output.mp4`: Output file name.

Make sure the video and audio files have the same length for proper syncing. If not, you might need to trim or adjust them accordingly.

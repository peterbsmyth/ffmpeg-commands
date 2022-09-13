# ffmpeg-commands

[Using ffmpeg to cut video](https://superuser.com/questions/138331/using-ffmpeg-to-cut-up-video)  
[Using ffmpeg to concatenate video](https://trac.ffmpeg.org/wiki/Concatenate)  
[Using ffmpeg to extract a single image](https://stackoverflow.com/questions/27568254/how-to-extract-1-screenshot-for-a-video-with-ffmpeg-at-a-given-time)

# ffmpeg -i "output.mp4" -i "output (2).mp4" -filter_complex "[1:v]scale=256:256[v2];[0:v][v2]overlay=main_w-overlay_w-0:0" -c:v libx264 -c:a copy "output.mp4"
# ffmpeg -i "output.mp4" -i "output (3).mp4" -filter_complex "[1:v]scale=256:256[v2];[0:v][v2]overlay=main_w-overlay_w-0:0" -c:v libx264 -c:a copy "output.mp4"
# ffmpeg -i "output.mp4" -i "output (4).mp4" -filter_complex "[1:v]scale=256:256[v2];[0:v][v2]overlay=main_w-overlay_w-0:0" -c:v libx264 -c:a copy "output.mp4"
# ffmpeg -i "output.mp4" -i "output (5).mp4" -filter_complex "[1:v]scale=256:256[v2];[0:v][v2]overlay=main_w-overlay_w-0:0" -c:v libx264 -c:a copy "output.mp4"
# ffmpeg -i "output.mp4" -i "output (6).mp4" -filter_complex "[1:v]scale=256:256[v2];[0:v][v2]overlay=main_w-overlay_w-0:0" -c:v libx264 -c:a copy "output.mp4"
# ffmpeg -i "output.mp4" -i "output (7).mp4" -filter_complex "[1:v]scale=256:256[v2];[0:v][v2]overlay=main_w-overlay_w-0:0" -c:v libx264 -c:a copy "output.mp4"
# ffmpeg -i "output.mp4" -i "output (8).mp4" -filter_complex "[1:v]scale=256:256[v2];[0:v][v2]overlay=main_w-overlay_w-0:0" -c:v libx264 -c:a copy "output.mp4"
# ffmpeg -i "output.mp4" -i "output (9).mp4" -filter_complex "[1:v]scale=256:256[v2];[0:v][v2]overlay=main_w-overlay_w-0:0" -c:v libx264 -c:a copy "output.mp4"

# what is this doing?
## general
### -i defines an input
### -f defines input/output format [link](https://ffmpeg.org/ffmpeg-all.html#toc-Main-options)
### -itsoffset delays an input's video streams
### -filter_complex combines indidivudal filters using a filtergraph
### -map used to choose which streams from the input are to be used in the output, can also be used to exclude streams [link](https://trac.ffmpeg.org/wiki/Map)
### -codec:v used to set a video codec. alias -c:v
### -codec:a used to set an audio codec. alias -c:a

## filters [guide](https://trac.ffmpeg.org/wiki/FilteringGuide)
### **hstack** stacks input video horizontally [link](https://ffmpeg.org/ffmpeg-filters.html#hstack)
### **hstack** stacks input video vertically [link](https://ffmpeg.org/ffmpeg-filters.html#vstack)
### **scale** resizes input video 
### **overlay** overlays one video on top of another, takes in two inputs, the first is the main and the second is the overlay 
#### **x** is the x coordinate of the overlay on the main [link](https://ffmpeg.org/ffmpeg-filters.html#overlay-1)
#### **y** is the y coordinate of the overlay on the main [link](https://ffmpeg.org/ffmpeg-filters.html#overlay-1)
#### **shortest** if set to 1 then forces the output to terminate when the shortest input terminates
#### **format** set the format, defaults to YUV420 [link](https://ffmpeg.org/ffmpeg-filters.html#overlay-1)
#### **t** the timestamp, expressed in seconds
### **setpts** changes the presentation timestamp, pts


## notes for filters
### setpts=PTS-STARTPTS means start the presentation timestamp from 0 
### setpts=PTS+10/TB will offset the input by 10 seconds
### `overlay=enable='between(t,10,3*60)'` roughly means to apply the overlay filter between 10 seconds and 3 minutes
### `overlay=enable='gte(t,3)'` roughly means to apply the overlay filter starting from 3 seconds until the end of the input
### in the beginning of a filter [0] roughly means the first input by zero index. 
### in the end of a filter [out] roughly means the name of the output of the filter is [out].
### [0][1]overlay=enable='between(t,10,3*60)'[out] roughly means for the first input as the main and the second input as the overlaid, enable the overlay filter starting from 10 seconds in for the main and ending at 3 minutes in then finally name the output out
### [0:v][1:a]overlay roughly means use the video stream of the main and the audio stream of the overlay

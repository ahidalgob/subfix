# subfix

The subtitles you find for your super-legally-downloaded movie/show aren't correctly synced? This simple python3 tool aims for fixing them. It offers two ways to use it:

## Simple Sync
For this mode, just give the srt file as the argument for the script. You will be asked which subtitle frame you want to use as a sync-point and the desired time for that frame. **Simple**. Example:
`subfix subs.srt`

## Awesome Sync
For this mode, give both the srt and the video file as arguments (in that order). And... done. **Awesome**. Example: 
`subfix subs.srt movie.mkv` (the video format doesn't have to be mkv, just an example)

### Notes:
This tool is only capable of *shifting* the entire srt file. So if for example, the subtitles are synced in one part but out of time in another, this tool won't correctly fix them.

For the Awesome Sync to work you must provide *IBM Watson Speech to Text* credentials (You can get a free trial for 30 days and then still get some free use of the service each month). You should put the credentials on the credentials.py file.

Awesome Sync works only in English (though it can be easily extended).

Awesome Sync probably won't work very good with videos with few dialogues.

### Installation
Just clone the repo or download the script, probably you will need to give execution permissions to it. Install the requirements using `pip3` and you're ready to use the script.


## How the Awesome Sync works
The script gets some portions of audio from the file and sends them to *IBM Watson Speech to Text Service*. Then the script tries to find the most suitable shift, this is done trying different shifts and getting a score for each one, using an algorithm similar to the one used in the classical problem *Edit Distance* (Dynamic Programming). Since the text in the srt file will be potentially much longer than the one transcribed, it's desirable to quickly "go over" a lot of subtitles frames while we're computing a shift score, this is done using simple binary search, which dramatically decreased the runtime.


This tool is by no means developed to its full potential. It was intended primarily to play around with IBM Watson Service and because the problem of getting the best shift seemed interesting to me (and I still think that way).

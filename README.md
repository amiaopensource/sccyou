# sccyou
A script that interprets the results of FFmpeg's [readeia608](https://ffmpeg.org/ffmpeg-filters.html#readeia608) filter to create scc (and optionally srt) outputs from standard definition video files which contain [EIA-608](https://en.wikipedia.org/wiki/EIA-608) data.

## Dependencies

ffmpeg 4.3 or later

## Usage

To use sccyou, simply download the script from the repo, make it executable (`chmod 755 sccyou.sh`), and run one of the following commands:

```
  ./sccyou.sh -h               display the help menu
  ./sccyou.sh INPUT_FILE       create an scc output
  ./sccyou.sh -s  INPUT_FILE   create both scc and srt outputs
  ./sccyou.sh -y  INPUT_FILE   overwrite any existing outputs
```
The results of sccyou will vary based upon your specific command, but will look like sidecar `INPUT_FILE.scc` and `INPUT_FILE.srt` files.

## Playback
After creating your sidecar files, sccyou will provide instructions for two forms of playback with captions (using `ffplay`).

Standard playback, with the captioned text on screen:
```
ffplay "INPUT_FILE" -vf subtitles="INPUT_FILE.scc"
```

![Alt text](./playback_standardcaptions.png "Standard Playback w/ ffplay")


Zoomed-in playback of caption data, scrolling vertically, with the captioned text appearing on screen:

```
ffplay "INPUT_FILE" -vf format=rgb24,crop=iw:1:0:1,scale=iw:4:flags=neighbor,tile=layout=1x120:overlap=119:init_padding=119,setdar=4/3,subtitles="INPUT_FILE.scc"
```

![Alt text](./playback_zoomedin.png "Zoomed in Playback w/ ffplay")


## Tell me more about closed captions

Adobe's [Introduction to Closed Captions](https://www.adobe.com/content/dam/acom/en/devnet/video/pdfs/introduction_to_closed_captions.pdf) offers a good technical introduction to the various closed captioning formats that are out there. 
Please note: this script will only work with video files that contain EIA-608 (also known as CEA-608 or "line 21") captions, which were used exclusively in NTSC television broadcasts.


More information about the scc format (hexadecimal character codes and sets) can be found [here](http://www.theneitherworld.com/mcpoodle/SCC_TOOLS/DOCS/).


## Feedback and Issues
We welcome any feedback, in the [Issues](https://github.com/amiaopensource/sccyou/issues) section of this repo, though keep in mind that EIA-608 captions were often improperly created/duplicated, and ffmpeg can only retrieve that which isn't total trash.


## Code Contributors
Dave Rice

Paul Mahol

## Sponsors
Development of sccyou was provided by New York Public Library's 2018/19 Innovation Project, and supported in part by the Charles H. Revson Foundation.


## Code of Conduct

You can read our contributor code of conduct [here](https://www.contributor-covenant.org/version/2/0/code_of_conduct/).

## License

sccyou is licensed under <a rel="license" href="https://opensource.org/licenses/MIT">The MIT License</a>.<br>

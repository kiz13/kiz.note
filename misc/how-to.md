# *

(reddit) [un-upvote old posts?](https://www.reddit.com/r/help/comments/2hym5x/how_to_unupvote_old_posts/) After 6 months posts/comments are archived, and it saves the vote scores. So you can't change your vote.

(SoundCloud) [you can only stream music or audio on one device at a time, If you are playing a track on one device, and try to play a track on another device that you are signed into, your first device will stop playing](https://help.soundcloud.com/hc/en-us/articles/115003563808-Listening-on-multiple-devices)

## convert bitmap to vector

e.g. png => svg

- with [inkscape](https://inkscape.org/), or 
- from the command line, PNG => PNM => SVG
  1. install [potrace](http://potrace.sourceforge.net/) and [magick](https://imagemagick.org/index.php)
  2. `magick file.png file.pnm`
  3. `potrace file.pnm -s -o file.svg`

[how to convert a png image to a svg?](https://stackoverflow.com/questions/1861382/how-to-convert-a-png-image-to-a-svg)

[conversion of SVG into PNG and vice versa](https://stackoverflow.com/questions/4021756/conversion-of-svg-into-png-jpeg-bmp-and-vice-versa)

[how to retain color using potrace?](https://superuser.com/questions/1544218/how-to-retain-color-when-using-potrace)

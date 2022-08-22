# *

use of <kbd>Shift</kbd> + scroll wheel is common for horizontal scrolling

[obs 怎么用](https://www.zhihu.com/question/265231508/answer/588785627)

[copying an url from browser's address bar gives encoded one?](https://stackoverflow.com/questions/18176661/copying-a-utf-8-url-from-browsers-address-bar-gives-only-the-ugly-encoded-one)

VisualVM, change the displaying font size? Start VisualVM with the `--fontsize` parameter: `visualvm --fontsize 15`. For a permanent change, add this parameter to the visualvm_default_options in `<visualvm_install>/etc/visualvm.conf`. [gitter source](https://gitter.im/VisualVM/Feedback?at=5feaf7612084ee4b787b9fde)

## JMeter

使用 JMeter [ref1](https://www.cnblogs.com/stulzq/p/8971531.html) and [ref2](https://www.cnblogs.com/dinghanhua/p/5646435.html)

send increment value on each request?
- [use _User Parameters_](https://stackoverflow.com/questions/52000899/jmeter-increment-value-before-each-sampler-request)
- inside json, `"key"="${__intSum(,${__counter(,)},)}"` [source](https://sqa.stackexchange.com/a/49190)

the response body contains garbled (chinese) character | [响应结果乱码 \(51cto\)](https://blog.51cto.com/ydhome/1864340) HTTP Request > Add PostProcessor > BeanShell PostProcessor > `prev.setDataEncoding("UTF-8")`

[how to set both query parameters and request body?](https://stackoverflow.com/a/49430194/11844003) append parameters to the url, then set body data. You can ONLY fill data on one tab, Parameters or Body Data, not both. See so
- [is there a way to send both?](https://stackoverflow.com/questions/32956089/send-both-parameters-and-body-data-with-jmeter-http-request)
- [unable to click parameter tab after adding body data](https://stackoverflow.com/questions/68662259/jmeter-unable-to-click-parameter-tab-when-added-body-data)
- [you can send JSON payload in "Parameters"](https://stackoverflow.com/a/51609079/11844003)

## Chrome

(chrome) <kbd>Shift</kbd> + <kbd>Esc</kbd> opens task manager

chrome not opening any pages? Maybe some extension cause it, uninstall 'em to check.

[gee, view raw pdf using google docs](https://webapps.stackexchange.com/a/78367)

[cors error, the request client is not a secure context](https://stackoverflow.com/questions/66534759/chrome-cors-error-on-request-to-localhost-dev-server-from-remote-site)

## Ditto

- [Windows 10 局域网多设备共享剪贴板](https://blog.csdn.net/GentleCP/article/details/109022869)

## Firefox

- ["Tab to Search" functionality into FF](https://support.mozilla.org/en-US/questions/1177556)

- [show the datetime when viewing history](https://support.mozilla.org/en-US/questions/1197226)

- [Dark mode for Firefox's built-in PDF viewer](https://pncnmnp.github.io/blogs/firefox-dark-mode.html)

  ```css
  #viewerContainer > #viewer > .page > .canvasWrapper > canvas {
      /* source https://css-tricks.com/almanac/properties/f/filter/
      filter: xxx
      */
  }
  ```

## Notepad3

- [Multi-tab mode](https://github.com/rizonesoft/Notepad3/issues/2525) requests

## Postman

[Runner removes the leading 0's from .csv data](https://github.com/postmanlabs/postman-app-support/issues/2734)

> We convert numbers without quotes in CVS file into JavaScript Number while parsing the CVS file in the Postman Apps.

[post image?](https://stackoverflow.com/questions/39660074/post-image-data-using-postman)

[import cURL?](https://stackoverflow.com/questions/27957943/simulate-a-specific-curl-in-postman) click Import on the upper left side | switch to Raw text tab | paste cURL | go

[where are collections saved?](https://stackoverflow.com/questions/47399809/where-are-postman-collections-saved)

## Spotify

- [ ] [bg color of lyrics is way too bright sometimes](https://community.spotify.com/t5/Closed-Ideas/Background-color-of-lyrics-is-hurting-my-eyes/idi-p/5210449) \*\*eyesore\*\*
- [ ] after viewing a singer's profile, I press the back button, it scrolls to the bottom of the previous page [check this](https://community.spotify.com/t5/Desktop-Windows/Bug-scroll-goes-to-the-bottom-of-quot-Overview-quot/td-p/1688143)
- [x] [my phone controls volume on my pc?](https://community.spotify.com/t5/Android/How-to-stop-my-phone-from-controlling-volume-on-my-computer/td-p/5080352) with the Spotify app open on both the pc and phone you can control the playback of the desktop app, so you need to close the Spotify app on your phone.
- Jakub Steplowski's [SpotifyLyricsNET](https://github.com/JakubSteplowski/SpotifyLyricsNET) repo is deleted, now it's [versefy](https://versefy.app/)

---

- [how to put all songs into a playlist](https://community.spotify.com/t5/Desktop-Mac/How-to-put-all-my-songs-into-a-playlist/td-p/1079311)
- [perfectionism, organize your music](https://community.spotify.com/t5/Chat/Perfectionism-How-do-you-organize-your-music/td-p/1201032)
- [synchronize local files on iOS](https://community.spotify.com/t5/FAQs/Local-Files/ta-p/5186118/redirect_from_archived_page/true)
- [when and how does Spotify count songs as **listened**](https://community.spotify.com/t5/Accounts/When-and-how-does-Spotify-count-songs-as-quot-listened-to-quot/td-p/952243)

## Telegram

Telegram ... re-encoding all GIFs to mpeg4 videos that require up to 95% less disk space for the same image quality.

## Evernote

已经不用了

- [x] version 10.8.5 evernote [global keyboard shortcuts discussion](https://discussion.evernote.com/forums/topic/131211-disable-global-keyboard-shortcuts/)
- [ ] evernote high cpu usage even after quit the app

---

- 搜索栏 [Quotation marks return results with an exact match](https://help.evernote.com/hc/en-us/articles/208313828-How-to-use-Evernote-s-advanced-search-syntax)
- [insert symbols or emojis](https://discussion.evernote.com/topic/118365-how-do-i-insert-symbols-or-emojis/?do=findComment&comment=531270) in Evernote

## Notable

已经不用了

- [ ] split-view scrolling position synchronization [check](https://github.com/notable/notable/issues/311)
- [ ] [real dark mode](https://github.com/rizonesoft/Notepad3/issues/1811)

## end

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

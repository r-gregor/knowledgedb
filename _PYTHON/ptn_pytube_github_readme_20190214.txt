filename: ptn_pytube_github_readme_20190214.txt
https://github.com/nficano/pytube

nficano/pytube

README.md

pytube
   pytube is a very serious, lightweight, dependency-free Python library (and command-line utility) for
   downloading YouTube Videos.

Description
   YouTube is the most popular video-sharing platform in the world and as a hacker you may encounter a
   situation where you want to script something to download videos. For this I present to you pytube.

   pytube is a lightweight library written in Python. It has no third party dependencies and aims to be
   highly reliable.

   pytube also makes pipelining easy, allowing you to specify callback functions for different download
   events, such as on progress or on complete.

   Finally pytube also includes a command-line utility, allowing you to quickly download videos right
   from terminal.

Behold, a perfect balance of simplicity versus flexibility:
 >>> YouTube('https://youtu.be/9bZkp7q19f0').streams.first().download()
 >>> yt = YouTube('http://youtube.com/watch?v=9bZkp7q19f0')
 >>> yt.streams
  ... .filter(progressive=True, file_extension='mp4')
  ... .order_by('resolution')
  ... .desc()
  ... .first()
  ... .download()

Features
     * Support for Both Progressive & DASH Streams
     * Support for downloading complete playlist
     * Easily Register on_download_progress & on_download_complete callbacks
     * Command-line Interfaced Included
     * Caption Track Support
     * Outputs Caption Tracks to .srt format (SubRip Subtitle)
     * Ability to Capture Thumbnail URL.
     * Extensively Documented Source Code
     * No Third-Party Dependencies

Installation
   Download using pip via pypi.
$ pip install pytube

Getting started
   Let's begin with showing how easy it is to download a video with pytube:
>>> from pytube import YouTube
>>> YouTube('http://youtube.com/watch?v=9bZkp7q19f0').streams.first().download()

   This example will download the highest quality progressive download stream available.

   Next, let's explore how we would view what video streams are available:
>>> yt = YouTube('http://youtube.com/watch?v=9bZkp7q19f0')
>>> yt.streams.all()
 [<Stream: itag="22" mime_type="video/mp4" res="720p" fps="30fps" vcodec="avc1.64001F" acodec="mp4a.40.2">,
 <Stream: itag="43" mime_type="video/webm" res="360p" fps="30fps" vcodec="vp8.0" acodec="vorbis">,
 <Stream: itag="18" mime_type="video/mp4" res="360p" fps="30fps" vcodec="avc1.42001E" acodec="mp4a.40.2">,
 <Stream: itag="36" mime_type="video/3gpp" res="240p" fps="30fps" vcodec="mp4v.20.3" acodec="mp4a.40.2">,
 <Stream: itag="17" mime_type="video/3gpp" res="144p" fps="30fps" vcodec="mp4v.20.3" acodec="mp4a.40.2">,
 <Stream: itag="137" mime_type="video/mp4" res="1080p" fps="30fps" vcodec="avc1.640028">,
 <Stream: itag="248" mime_type="video/webm" res="1080p" fps="30fps" vcodec="vp9">,
 <Stream: itag="136" mime_type="video/mp4" res="720p" fps="30fps" vcodec="avc1.4d401f">,
 <Stream: itag="247" mime_type="video/webm" res="720p" fps="30fps" vcodec="vp9">,
 <Stream: itag="135" mime_type="video/mp4" res="480p" fps="30fps" vcodec="avc1.4d401e">,
 <Stream: itag="244" mime_type="video/webm" res="480p" fps="30fps" vcodec="vp9">,
 <Stream: itag="134" mime_type="video/mp4" res="360p" fps="30fps" vcodec="avc1.4d401e">,
 <Stream: itag="243" mime_type="video/webm" res="360p" fps="30fps" vcodec="vp9">,
 <Stream: itag="133" mime_type="video/mp4" res="240p" fps="30fps" vcodec="avc1.4d4015">,
 <Stream: itag="242" mime_type="video/webm" res="240p" fps="30fps" vcodec="vp9">,
 <Stream: itag="160" mime_type="video/mp4" res="144p" fps="30fps" vcodec="avc1.4d400c">,
 <Stream: itag="278" mime_type="video/webm" res="144p" fps="30fps" vcodec="vp9">,
 <Stream: itag="140" mime_type="audio/mp4" abr="128kbps" acodec="mp4a.40.2">,
 <Stream: itag="171" mime_type="audio/webm" abr="128kbps" acodec="vorbis">,
 <Stream: itag="249" mime_type="audio/webm" abr="50kbps" acodec="opus">,
 <Stream: itag="250" mime_type="audio/webm" abr="70kbps" acodec="opus">,
 <Stream: itag="251" mime_type="audio/webm" abr="160kbps" acodec="opus">]

   You may notice that some streams listed have both a video codec and audio codec, while others have
   just video or just audio, this is a result of YouTube supporting a streaming technique called Dynamic
   Adaptive Streaming over HTTP (DASH).

   In the context of pytube, the implications are for the highest quality streams; you now need to
   download both the audio and video tracks and then post-process them with software like FFmpeg to
   merge them.

   The legacy streams that contain the audio and video in a single file (referred to as "progressive
   download") are still available, but only for resolutions 720p and below.

   To only view these progressive download streams:
 >>> yt.streams.filter(progressive=True).all()
  [<Stream: itag="22" mime_type="video/mp4" res="720p" fps="30fps" vcodec="avc1.64001F" acodec="mp4a.40.2">,
  <Stream: itag="43" mime_type="video/webm" res="360p" fps="30fps" vcodec="vp8.0" acodec="vorbis">,
  <Stream: itag="18" mime_type="video/mp4" res="360p" fps="30fps" vcodec="avc1.42001E" acodec="mp4a.40.2">,
  <Stream: itag="36" mime_type="video/3gpp" res="240p" fps="30fps" vcodec="mp4v.20.3" acodec="mp4a.40.2">,
  <Stream: itag="17" mime_type="video/3gpp" res="144p" fps="30fps" vcodec="mp4v.20.3" acodec="mp4a.40.2">]

   Conversely, if you only want to see the DASH streams (also referred to as 'adaptive') you can do:
>>> yt.streams.filter(adaptive=True).all()
 [<Stream: itag="137" mime_type="video/mp4" res="1080p" fps="30fps" vcodec="avc1.640028">,
  <Stream: itag="248" mime_type="video/webm" res="1080p" fps="30fps" vcodec="vp9">,
  <Stream: itag="136" mime_type="video/mp4" res="720p" fps="30fps" vcodec="avc1.4d401f">,
  <Stream: itag="247" mime_type="video/webm" res="720p" fps="30fps" vcodec="vp9">,
  <Stream: itag="135" mime_type="video/mp4" res="480p" fps="30fps" vcodec="avc1.4d401e">,
  <Stream: itag="244" mime_type="video/webm" res="480p" fps="30fps" vcodec="vp9">,
  <Stream: itag="134" mime_type="video/mp4" res="360p" fps="30fps" vcodec="avc1.4d401e">,
  <Stream: itag="243" mime_type="video/webm" res="360p" fps="30fps" vcodec="vp9">,
  <Stream: itag="133" mime_type="video/mp4" res="240p" fps="30fps" vcodec="avc1.4d4015">,
  <Stream: itag="242" mime_type="video/webm" res="240p" fps="30fps" vcodec="vp9">,
  <Stream: itag="160" mime_type="video/mp4" res="144p" fps="30fps" vcodec="avc1.4d400c">,
  <Stream: itag="278" mime_type="video/webm" res="144p" fps="30fps" vcodec="vp9">,
  <Stream: itag="140" mime_type="audio/mp4" abr="128kbps" acodec="mp4a.40.2">,
  <Stream: itag="171" mime_type="audio/webm" abr="128kbps" acodec="vorbis">,
  <Stream: itag="249" mime_type="audio/webm" abr="50kbps" acodec="opus">,
  <Stream: itag="250" mime_type="audio/webm" abr="70kbps" acodec="opus">,
  <Stream: itag="251" mime_type="audio/webm" abr="160kbps" acodec="opus">]

   You can also download a complete Youtube playlist:
>>> from pytube import Playlist
>>> pl = Playlist("https://www.youtube.com/watch?v=Edpy1szoG80&list=PL153hDY-y1E00uQtCVCVC8xJ25TYX8yPU")
>>> pl.download_all()
>>> # or if you want to download in a specific directory
>>> pl.download_all('/path/to/directory/')

   This will download the highest progressive stream available (generally 720p) from the given playlist.
   Later more options would be given for user's flexibility to choose video resolution.

   Pytube allows you to filter on every property available (see the documentation for the complete
   list), let's take a look at some of the most useful ones.

   To list the audio only streams:
>>> yt.streams.filter(only_audio=True).all()
  [<Stream: itag="140" mime_type="audio/mp4" abr="128kbps" acodec="mp4a.40.2">,
  <Stream: itag="171" mime_type="audio/webm" abr="128kbps" acodec="vorbis">,
  <Stream: itag="249" mime_type="audio/webm" abr="50kbps" acodec="opus">,
  <Stream: itag="250" mime_type="audio/webm" abr="70kbps" acodec="opus">,
  <Stream: itag="251" mime_type="audio/webm" abr="160kbps" acodec="opus">]

   To list only mp4 streams:
>>> yt.streams.filter(subtype='mp4').all()
 [<Stream: itag="22" mime_type="video/mp4" res="720p" fps="30fps" vcodec="avc1.64001F" acodec="mp4a.40.2">,
  <Stream: itag="18" mime_type="video/mp4" res="360p" fps="30fps" vcodec="avc1.42001E" acodec="mp4a.40.2">,
  <Stream: itag="137" mime_type="video/mp4" res="1080p" fps="30fps" vcodec="avc1.640028">,
  <Stream: itag="136" mime_type="video/mp4" res="720p" fps="30fps" vcodec="avc1.4d401f">,
  <Stream: itag="135" mime_type="video/mp4" res="480p" fps="30fps" vcodec="avc1.4d401e">,
  <Stream: itag="134" mime_type="video/mp4" res="360p" fps="30fps" vcodec="avc1.4d401e">,
  <Stream: itag="133" mime_type="video/mp4" res="240p" fps="30fps" vcodec="avc1.4d4015">,
  <Stream: itag="160" mime_type="video/mp4" res="144p" fps="30fps" vcodec="avc1.4d400c">,
  <Stream: itag="140" mime_type="audio/mp4" abr="128kbps" acodec="mp4a.40.2">]

   Multiple filters can also be specified:
>>> yt.streams.filter(subtype='mp4', progressive=True).all()
>>> # this can also be expressed as:
>>> yt.streams.filter(subtype='mp4').filter(progressive=True).all()
  [<Stream: itag="22" mime_type="video/mp4" res="720p" fps="30fps" vcodec="avc1.64001F" acodec="mp4a.40.2">,
  <Stream: itag="18" mime_type="video/mp4" res="360p" fps="30fps" vcodec="avc1.42001E" acodec="mp4a.40.2">]

   You also have an interface to select streams by their itag, without needing to filter:
>>> yt.streams.get_by_itag(22)
  <Stream: itag="22" mime_type="video/mp4" res="720p" fps="30fps" vcodec="avc1.64001F" acodec="mp4a.40.2">

   If you need to optimize for a specific feature, such as the "highest resolution" or "lowest average
   bitrate":
>>> yt.streams.filter(progressive=True).order_by('resolution').desc().all()

   Note that order_by cannot be used if your attribute is undefined in any of the Stream instances, so
   be sure to apply a filter to remove those before calling it.

   If your application requires post-processing logic, pytube allows you to specify an "on download
   complete" callback function:
 >>> def convert_to_aac(stream, file_handle):
         return  # do work

 >>> yt.register_on_complete_callback(convert_to_aac)

   Similarly, if your application requires on-download progress logic, pytube exposes a callback for
   this as well:
 >>> def show_progress_bar(stream, chunk, file_handle, bytes_remaining):
         return  # do work

 >>> yt.register_on_progress_callback(show_progress_bar)

Command-line interface

   pytube also ships with a tiny cli interface for downloading and probing videos.

   Let's start with downloading:
$ pytube http://youtube.com/watch?v=9bZkp7q19f0 --itag=22

   To view available streams:
$ pytube http://youtube.com/watch?v=9bZkp7q19f0 --list

   Finally, if you're filing a bug report, the cli contains a switch called --build-playback-report,
   which bundles up the state, allowing others to easily replay your issue.

     * C 2019 GitHub, Inc.
     * Terms
     * Privacy
     * Security
     * Status
     * Help

     * Contact GitHub
     * Pricing
     * API
     * Training
     * Blog
     * About

   (BUTTON) You can't perform that action at this time.

   You signed in with another tab or window. Reload to refresh your session. You signed out in
   another tab or window. Reload to refresh your session.

   (BUTTON)

   Press h to open a hovercard with more details.

References

   Visible links
   1. https://github.com/opensearch.xml
   2. https://github.com/nficano/pytube/commits/master.atom
   3. https://github.com/nficano/pytube#start-of-content
   4. https://github.com/features
   5. https://github.com/features/code-review/
   6. https://github.com/features/project-management/
   7. https://github.com/features/integrations
   8. https://github.com/features/actions
   9. https://github.com/features#team-management
  10. https://github.com/features#social-coding
  11. https://github.com/features#documentation
  12. https://github.com/features#code-hosting
  13. https://github.com/case-studies
  14. https://github.com/security
  15. https://github.com/enterprise
  16. https://github.com/explore
  17. https://github.com/topics
  18. https://github.com/collections
  19. https://github.com/trending
  20. https://lab.github.com/
  21. https://opensource.guide/
  22. https://github.com/events
  23. https://github.community/
  24. https://education.github.com/
  25. https://github.com/marketplace
  26. https://github.com/pricing
  27. https://github.com/pricing#feature-comparison
  28. https://enterprise.github.com/contact
  29. https://github.com/nonprofit
  30. https://education.github.com/
  31. https://github.com/login?return_to=%2Fnficano%2Fpytube
  32. https://github.com/join
  33. https://github.com/login?return_to=%2Fnficano%2Fpytube
  34. https://github.com/nficano/pytube/watchers
  35. https://github.com/login?return_to=%2Fnficano%2Fpytube
  36. https://github.com/nficano/pytube/stargazers
  37. https://github.com/login?return_to=%2Fnficano%2Fpytube
  38. https://github.com/nficano/pytube/network/members
  39. https://github.com/nficano
  40. https://github.com/nficano/pytube
  41. https://github.com/nficano/pytube
  42. https://github.com/nficano/pytube/issues
  43. https://github.com/nficano/pytube/pulls
  44. https://github.com/nficano/pytube/wiki
  45. https://github.com/nficano/pytube/pulse
  46. https://github.com/join?source=prompt-code
  47. https://python-pytube.readthedocs.io/
  48. https://github.com/topics/python
  49. https://github.com/topics/youtube
  50. https://github.com/topics/pythonic
  51. https://github.com/topics/api-wrapper
  52. https://github.com/nficano/pytube/commits/master
  53. https://github.com/nficano/pytube/branches
  54. https://github.com/nficano/pytube/releases
  55. https://github.com/nficano/pytube/graphs/contributors
  56. https://github.com/nficano/pytube/blob/master/LICENSE
  57. https://github.com/nficano/pytube/search?l=python
  58. https://github.com/nficano/pytube/search?l=makefile
  59. https://github.com/nficano/pytube/find/master
  60. https://github.com/nficano/pytube/archive/master.zip
  61. https://desktop.github.com/
  62. https://desktop.github.com/
  63. https://developer.apple.com/xcode/
  64. https://visualstudio.github.com/
  65. https://github.com/nficano
  66. https://github.com/nficano/pytube/commits?author=nficano
  67. https://github.com/nficano/pytube/commit/aac8ac91918ea9273cf3667b1f397ae4ddb348b5
  68. https://github.com/nficano/pytube/pull/355
  69. https://github.com/nficano/pytube/commit/aac8ac91918ea9273cf3667b1f397ae4ddb348b5
  70. https://github.com/nficano/pytube/commit/aac8ac91918ea9273cf3667b1f397ae4ddb348b5
  71. https://github.com/nficano/pytube/tree/aac8ac91918ea9273cf3667b1f397ae4ddb348b5
  72. https://github.com/nficano/pytube/tree/master/docs
  73. https://github.com/nficano/pytube/commit/21cb640f034e559bcacef54c3c3c31734e655e1f
  74. https://github.com/nficano/pytube/tree/master/images
  75. https://github.com/nficano/pytube/commit/6daa0e6d078bdbea32f60002f17403c2ad932e8e
  76. https://github.com/nficano/pytube/tree/master/pytube
  77. https://github.com/nficano/pytube/commit/702408d1a6c4cbd67e3a27be958ee23914ef4a0c
  78. https://github.com/nficano/pytube/tree/master/tests
  79. https://github.com/nficano/pytube/commit/536d58109aaae1f11ce38ba7b6781a75b2773395
  80. https://github.com/nficano/pytube/blob/master/.envrc
  81. https://github.com/nficano/pytube/commit/6f8e5d3e0511b1c02e3dea7b5db0f9d6c626ff02
  82. https://github.com/nficano/pytube/blob/master/.gitattributes
  83. https://github.com/nficano/pytube/commit/038cd4fb2e4cf50b1f63679066e0557ece6296b7
  84. https://github.com/nficano/pytube/blob/master/.gitignore
  85. https://github.com/nficano/pytube/commit/cf2a40242d4385d4dcd39fae21be7bedcccce826
  86. https://github.com/nficano/pytube/blob/master/.pre-commit-config.yaml
  87. https://github.com/nficano/pytube/commit/860893c4095815dd332a413dfb3cb7929c35741f
  88. https://github.com/nficano/pytube/blob/master/.travis.yml
  89. https://github.com/nficano/pytube/commit/0fe65cfbcb1e7aa7fb0c432353a4d3dcfb2e8718
  90. https://github.com/nficano/pytube/blob/master/CODE_OF_CONDUCT.md
  91. https://github.com/nficano/pytube/commit/64a4e3a1a4d0274a5732c8e5fa7dde7255a64404
  92. https://github.com/nficano/pytube/blob/master/LICENSE
  93. https://github.com/nficano/pytube/commit/21cb640f034e559bcacef54c3c3c31734e655e1f
  94. https://github.com/nficano/pytube/blob/master/MANIFEST.in
  95. https://github.com/nficano/pytube/commit/60afa9f2419ea608ba507becd9e8ccee10af49f4
  96. https://github.com/nficano/pytube/blob/master/Makefile
  97. https://github.com/nficano/pytube/commit/b746f0ad0b33a94fd5ea1d3d9f00343fa3e55882
  98. https://github.com/nficano/pytube/blob/master/Pipfile
  99. https://github.com/nficano/pytube/commit/99c36c53a5b06d1872358b2eab696a179fa04302
 100. https://github.com/nficano/pytube/blob/master/Pipfile.lock
 101. https://github.com/nficano/pytube/commit/4aa2cbd1d31c479f6693f88fd4f3f2e6bb6dc2a3
 102. https://github.com/nficano/pytube/blob/master/README.md
 103. https://github.com/nficano/pytube/commit/07b5aa89673224aead2d396e7f57eab7a5be202c
 104. https://github.com/nficano/pytube/blob/master/setup.cfg
 105. https://github.com/nficano/pytube/commit/b746f0ad0b33a94fd5ea1d3d9f00343fa3e55882
 106. https://github.com/nficano/pytube/blob/master/setup.py
 107. https://github.com/nficano/pytube/commit/c38f6f51f76b3be018482aec692bac58f9af2067
 108. https://github.com/nficano/pytube/blob/master/images/pytube.png?raw=true
 109. https://camo.githubusercontent.com/42bf25132fa007e1d03dea53f6a36d8266c80fe8/68747470733a2f2f696d672e736869656c64732e696f2f707970692f762f7079747562652e737667
 110. https://travis-ci.org/nficano/pytube
 111. http://python-pytube.readthedocs.io/en/latest/?badge=latest
 112. https://coveralls.io/github/nficano/pytube?branch=master
 113. https://pypi.org/project/pytube/
 114. https://pypi.python.org/pypi/pytube/
 115. https://github.com/site/terms
 116. https://github.com/site/privacy
 117. https://github.com/security
 118. https://githubstatus.com/
 119. https://help.github.com/
 120. https://github.com/contact
 121. https://github.com/pricing
 122. https://developer.github.com/
 123. https://training.github.com/
 124. https://github.blog/
 125. https://github.com/about
 126. https://github.com/nficano/pytube
 127. https://github.com/nficano/pytube

   Hidden links:
 128. https://github.com/
 129. https://github.com/nficano/pytube
 130. https://github.com/nficano/pytube
 131. https://github.com/nficano/pytube
 132. https://help.github.com/articles/which-remote-url-should-i-use
 133. https://github.com/nficano/pytube#pytube
 134. https://github.com/nficano/pytube#description
 135. https://github.com/nficano/pytube#behold-a-perfect-balance-of-simplicity-versus-flexibility
 136. https://github.com/nficano/pytube#features
 137. https://github.com/nficano/pytube#installation
 138. https://github.com/nficano/pytube#getting-started
 139. https://github.com/nficano/pytube#command-line-interface
 140. https://github.com/


---
https://python-pytube.readthedocs.io/en/latest/user/quickstart.html

pytube

Quickstart
   This guide will walk you through the basic usage of pytube.

   Let's get started with some examples.

Downloading a Video
   Downloading a video from YouTube with pytube is incredibly easy.

   Begin by importing the YouTube class:
>>> from pytube import YouTube

   Now, let's try to download a video. For this example, let's take something popular like PSY -
   Gangnam Style:
>>> yt = YouTube('https://www.youtube.com/watch?v=9bZkp7q19f0')

   Now, we have a YouTube object called yt.

   The pytube API makes all information intuitive to access. For example, this is how you would get the
   video's title:
>>> yt.title
PSY - GANGNAM STYLE(???????) M/V

   And this would be how you would get the thumbnail url:
>>> yt.thumbnail_url
'https://i.ytimg.com/vi/mTOYClXhJD0/default.jpg'

   Neat, right? Next let's see the available media formats:
>>> yt.streams.all()
[<Stream: itag="22" mime_type="video/mp4" res="720p" fps="30fps" vcodec="avc1.64001F" acodec="mp4a.40.2">,
<Stream: itag="43" mime_type="video/webm" res="360p" fps="30fps" vcodec="vp8.0" acodec="vorbis">,
<Stream: itag="18" mime_type="video/mp4" res="360p" fps="30fps" vcodec="avc1.42001E" acodec="mp4a.40.2">,
<Stream: itag="36" mime_type="video/3gpp" res="240p" fps="30fps" vcodec="mp4v.20.3" acodec="mp4a.40.2">,
<Stream: itag="17" mime_type="video/3gpp" res="144p" fps="30fps" vcodec="mp4v.20.3" acodec="mp4a.40.2">,
<Stream: itag="137" mime_type="video/mp4" res="1080p" fps="30fps" vcodec="avc1.640028">,
<Stream: itag="136" mime_type="video/mp4" res="720p" fps="30fps" vcodec="avc1.4d401f">,
<Stream: itag="135" mime_type="video/mp4" res="480p" fps="30fps" vcodec="avc1.4d401f">,
<Stream: itag="134" mime_type="video/mp4" res="360p" fps="30fps" vcodec="avc1.4d401e">,
<Stream: itag="133" mime_type="video/mp4" res="240p" fps="30fps" vcodec="avc1.4d4015">,
<Stream: itag="160" mime_type="video/mp4" res="144p" fps="30fps" vcodec="avc1.4d400c">,
<Stream: itag="140" mime_type="audio/mp4" abr="128kbps" acodec="mp4a.40.2">,
<Stream: itag="171" mime_type="audio/webm" abr="128kbps" acodec="vorbis">]

   Let's say we want to get the first stream:
>>> stream = yt.streams.first()
>>> stream
<Stream: itag="22" mime_type="video/mp4" res="720p" fps="30fps" vcodec="avc1.64001F" acodec="mp4a.40.2">

   And to download it to the current working directory:
>>> stream.download()

   You can also specify a destination path:
>>> stream.download('/tmp')

Working with Streams

   The next section will explore the various options available for working with media streams, but
   before we can dive in, we need to review a new-ish streaming technique adopted by YouTube.

DASH vs Progressive Streams

   Begin by running the following:
>>> yt.streams.all()
[<Stream: itag="22" mime_type="video/mp4" res="720p" fps="30fps" vcodec="avc1.64001F" acodec="mp4a.40.2">,
<Stream: itag="43" mime_type="video/webm" res="360p" fps="30fps" vcodec="vp8.0" acodec="vorbis">,
<Stream: itag="18" mime_type="video/mp4" res="360p" fps="30fps" vcodec="avc1.42001E" acodec="mp4a.40.2">,
<Stream: itag="36" mime_type="video/3gpp" res="240p" fps="30fps" vcodec="mp4v.20.3" acodec="mp4a.40.2">,
<Stream: itag="17" mime_type="video/3gpp" res="144p" fps="30fps" vcodec="mp4v.20.3" acodec="mp4a.40.2">,
<Stream: itag="137" mime_type="video/mp4" res="1080p" fps="30fps" vcodec="avc1.640028">,
<Stream: itag="136" mime_type="video/mp4" res="720p" fps="30fps" vcodec="avc1.4d401f">,
<Stream: itag="135" mime_type="video/mp4" res="480p" fps="30fps" vcodec="avc1.4d401f">,
<Stream: itag="134" mime_type="video/mp4" res="360p" fps="30fps" vcodec="avc1.4d401e">,
<Stream: itag="133" mime_type="video/mp4" res="240p" fps="30fps" vcodec="avc1.4d4015">,
<Stream: itag="160" mime_type="video/mp4" res="144p" fps="30fps" vcodec="avc1.4d400c">,
<Stream: itag="140" mime_type="audio/mp4" abr="128kbps" acodec="mp4a.40.2">,
<Stream: itag="171" mime_type="audio/webm" abr="128kbps" acodec="vorbis">]

   You may notice that some streams listed have both a video codec and audio codec, while others have
   just video or just audio, this is a result of YouTube supporting a streaming technique called Dynamic
   Adaptive Streaming over HTTP (DASH).

   In the context of pytube, the implications are for the highest quality streams; you now need to
   download both the audio and video tracks and then post-process them with software like FFmpeg to
   merge them.

   The legacy streams that contain the audio and video in a single file (referred to as "progressive
   download") are still available, but only for resolutions 720p and below.

   To only view these progressive download streams:
>>> yt.streams.filter(progressive=True).all()
[<Stream: itag="22" mime_type="video/mp4" res="720p" fps="30fps" vcodec="avc1.64001F" acodec="mp4a.40.2">,
<Stream: itag="43" mime_type="video/webm" res="360p" fps="30fps" vcodec="vp8.0" acodec="vorbis">,
<Stream: itag="18" mime_type="video/mp4" res="360p" fps="30fps" vcodec="avc1.42001E" acodec="mp4a.40.2">,
<Stream: itag="36" mime_type="video/3gpp" res="240p" fps="30fps" vcodec="mp4v.20.3" acodec="mp4a.40.2">,
<Stream: itag="17" mime_type="video/3gpp" res="144p" fps="30fps" vcodec="mp4v.20.3" acodec="mp4a.40.2">]

   Conversely, if you only want to see the DASH streams (also referred to as 'adaptive') you can do:
>>> yt.streams.filter(adaptive=True).all()
[<Stream: itag="137" mime_type="video/mp4" res="1080p" fps="30fps" vcodec="avc1.640028">,
<Stream: itag="136" mime_type="video/mp4" res="720p" fps="30fps" vcodec="avc1.4d401f">,
<Stream: itag="135" mime_type="video/mp4" res="480p" fps="30fps" vcodec="avc1.4d401f">,
<Stream: itag="134" mime_type="video/mp4" res="360p" fps="30fps" vcodec="avc1.4d401e">,
<Stream: itag="133" mime_type="video/mp4" res="240p" fps="30fps" vcodec="avc1.4d4015">,
<Stream: itag="160" mime_type="video/mp4" res="144p" fps="30fps" vcodec="avc1.4d400c">,
<Stream: itag="140" mime_type="audio/mp4" abr="128kbps" acodec="mp4a.40.2">,
<Stream: itag="171" mime_type="audio/webm" abr="128kbps" acodec="vorbis">]

   Pytube allows you to filter on every property available (see pytube.StreamQuery.filter() for a
   complete list of filter options), let's take a look at some common examples:

Query audio only Streams
   To query the streams that contain only the audio track:
>>> yt.streams.filter(only_audio=True).all()
[<Stream: itag="140" mime_type="audio/mp4" abr="128kbps" acodec="mp4a.40.2">,
<Stream: itag="171" mime_type="audio/webm" abr="128kbps" acodec="vorbis">]

Query MPEG-4 Streams
   To query only streams in the MPEG-4 format:
>>> yt.streams.filter(file_extension='mp4').all()
[<Stream: itag="22" mime_type="video/mp4" res="720p" fps="30fps" vcodec="avc1.64001F" acodec="mp4a.40.2">,
<Stream: itag="18" mime_type="video/mp4" res="360p" fps="30fps" vcodec="avc1.42001E" acodec="mp4a.40.2">,
<Stream: itag="137" mime_type="video/mp4" res="1080p" fps="30fps" vcodec="avc1.640028">,
<Stream: itag="136" mime_type="video/mp4" res="720p" fps="30fps" vcodec="avc1.4d401f">,
<Stream: itag="135" mime_type="video/mp4" res="480p" fps="30fps" vcodec="avc1.4d401f">,
<Stream: itag="134" mime_type="video/mp4" res="360p" fps="30fps" vcodec="avc1.4d401e">,
<Stream: itag="133" mime_type="video/mp4" res="240p" fps="30fps" vcodec="avc1.4d4015">,
<Stream: itag="160" mime_type="video/mp4" res="144p" fps="30fps" vcodec="avc1.4d400c">,
<Stream: itag="140" mime_type="audio/mp4" abr="128kbps" acodec="mp4a.40.2">]

Get Streams by itag
   To get a stream by a specific itag:
>>> yt.streams.get_by_itag('22')
<Stream: itag="22" mime_type="video/mp4" res="720p" fps="30fps" vcodec="avc1.64001F" acodec="mp4a.40.2">

Subtitle/Caption Tracks

   Pytube exposes the caption tracks in much the same way as querying the media streams. Let's begin
   by switching to a video that contains them:
>>> yt = YouTube('https://youtube.com/watch?v=XJGiS83eQLk')
>>> yt.captions.all()
[<Caption lang="Arabic" code="ar">,
<Caption lang="English (auto-generated)" code="en">,
<Caption lang="English" code="en">,
<Caption lang="English (United Kingdom)" code="en-GB">,
<Caption lang="German" code="de">,
<Caption lang="Greek" code="el">,
<Caption lang="Indonesian" code="id">,
<Caption lang="Sinhala" code="si">,
<Caption lang="Spanish" code="es">,
<Caption lang="Turkish" code="tr">]

   Now let's checkout the english captions:
>>> caption = yt.captions.get_by_language_code('en')

   Great, now let's see how YouTube formats them:
>>> caption.xml_captions
'<?xml version="1.0" encoding="utf-8" ?><transcript><text start="0" dur="5.541">well i&amp;#39...'

   Oh, this isn't very easy to work with, let's convert them to the srt format:
>>> print(caption.generate_srt_captions())
1
000:000:00,000 --> 000:000:05,541
well i'm just an editor and i dont know what to type

2
000:000:05,541 --> 000:000:12,321
not new to video. In fact, most films before 1930 were silent and used captions with video

---

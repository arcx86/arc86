+++
date = '2023-08-21T18:29:00+01:00'
lastmod = '2024-02-21T23:40:00Z'
draft = false
title = 'YouTube Archiving with yt-dlp'
tags = ['tech']
+++

Google has [updated their policy](http://web.archive.org/web/20230818191039/https://blog.google/technology/safety-security/updating-our-inactive-account-policies/) to delete accounts after 2 years of inactivity. Coupled with the rate at which channels are being terminated and videos removed for copyright violations or any number of other reasons, it's best to locally archive all videos you care about.

By far the best tool for this is [yt-dlp](https://github.com/yt-dlp/yt-dlp), a fork of [youtube-dl](https://github.com/ytdl-org/youtube-dl) which has also been [targeted with attempted takedowns](https://web.archive.org/web/20200329202929/https://torrentfreak.com/riaa-delists-youtube-rippers-from-google-using-rare-anti-circumvention-notices-191108/) in the past.

yt-dlp is a very simple command line-based tool for downloading and streaming videos from many platforms apart from just YouTube.

First, install the ```yt-dlp``` package from your package manager of choice.
On Windows 11, run ```winget install yt-dlp.yt-dlp``` in PowerShell/Terminal.
It's recommended to also install the ```ffmpeg``` package to allow encoding to various formats and containers.

The basic command to download a video is ```yt-dlp videourl``` which will download to your terminal session's current working directory.

This command can be used to archive entire playlists or channels by entering their url (```yt-dlp playlisturl```).

Private videos or playlists, such as your channel's liked videos, requires authenticating a login session.
The easiest way to achieve this is by loading a local copy of your YouTube session's cookies using the
```--cookies cookiesfile``` flag.

A cookies text file for YouTube can be generated with a browser extension such as [EditThisCookie](https://chrome.google.com/webstore/detail/editthiscookie/fngmhnnpilhplaeedifhccceomclgfbg/related) for Chromium-based browsers or [cookies.txt](https://addons.mozilla.org/en-US/firefox/addon/cookies-txt/) for Firefox.
From the extension, export the cookies to a text file such as ```cookies.txt``` to the directory you wish to download to.

If you plan to regularly back up a playlist such as your liked videos (manually or via a scheduled task/cronjob), it's also worth maintaining a download archive with the ```--download-archive archivefile``` flag.
This serves as a list of already downloaded videos, meaning that if the command is re-ran, it will skip all videos which have already been downloaded without throwing errors.

The full command to backup your private liked videos playlist to a set of files labelled with an index number, and to log all downloaded video addresses is:
```yt-dlp --download-archive "archive.txt" --cookies "cookies.txt" https://www.youtube.com/playlist?list=LL -o "%(playlist_index)s - %(title)s.%(ext)s"```
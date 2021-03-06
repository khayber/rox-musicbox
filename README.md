# Features#

  * MP3, OGG, Flac, WAV support.
  * ESD, Alsa, OSS support.
  * Album Art display
  * Drag and Drop adding of Songs, Directories of songs, and Playlists (m3u, pls and xml)
  * Shuffle play (with cache so you don't replay songs too frequently).
  * Seek control bar to zip to specific parts of any song.
  * Volume Control
  * Playlist filtering
  * Translations: fr, it, es, pt_BR

![http://rox-musicbox.googlecode.com/files/musicbox.png](http://rox-musicbox.googlecode.com/files/musicbox.png)

#Instructions#

Extract the MusicBox appdir and copy it to wherever you normally put ROX apps. Then launch it! Initially it assumes that you put all your mp3 and/or ogg files in ~/Music. If this is not correct you must edit the Options to suit your setup. For library changes just hit the refresh menu item, unless you used Drag and Drop in which case the display will update automatically. If you have a lot of files it will take considerable time to read them all - see below on how to speed things up. However, don't let that stop you from hitting the play button! We got threads!

In place of the ~/Music default library location you may enter

  * one or more directories separated by ':' like a path
  * one or more .pls or .m3u files
  * one or more .xml files (saved from MusicBox)
  * any combination of the above.

You can also leave it blank and just load files dynamically. This can be done in the following ways

  * Drag and Drop files or folders on the MusicBox main or Playlist windows
  * Pass files or folders or playlists on the MusicBox command line.
  * Use rpc (see below)

MusicBox currently exports the following commands via rpc

  * load_songs #replace existing and start playing
  * add_songs #append to existing
  * play
  * pause
  * next
  * prev
  * stop

Here is how to call these functions in python. Also, see the Extras directory for useful examples of this. We also support a similar set of command line options. (try: rox MusicBox -h)

#Tag Info and Filenames#

MusicBox will try to read tag info from your files, but this can take a long time and many files do not contain this information. Therefore, it will first attempt to 'guess' the artist, album and title from the filename and path of each song. However this loading process is a background task. You can start playing songs or even quit MusicBox while this is happening.

The default assumption is artist/album/title.ext, but you can change this if you need to. In the Options dialog there is a Pattern field that provides a place to edit the default pattern to be used. (Note: this is easy to get wrong and if you create a pattern that fails to match properly the default will be used) Currently MusicBox only supports artist, album, title and track.

The default pattern looks like this

    ^.*/(?P<artist>.*)/(?P<album>.*)/(?P<title>.*)


This pattern throws away any leading path, and separates the rest as artist/album/title. The <track> option is also available if you have track numbers as part of your file naming scheme.

MusicBox will also use Extended Attributes for tag info if available. These tags are my own creation and only are supported by my CD ripping application Ripper. Xattrs are not widely supported yet, but I believe these will be the future of metadata. Stay tuned.

#Libraries#

After loading a large list of songs, you can save these in a Library to speed up reloading the next time. To do this, right click on either the Main or Playlist windows and select Save. A ROX savebox will appear with Library.xml showing in the Choices (Options) folder for MusicBox. You may drag this file anywhere you want to save it and rename it if you wish. Be sure not to change the .xml extension or MusicBox will not know how to reload it. This file may now be dragged into either MusicBox window to reload those songs. MusicBox will not need to examine each file again to get the tag info - that was saved in the xml file. Loading times are much quicker this way. You can also use these files in the Options dialog as your default library instead of the path to the actual song files. You may create as many of library xml files as you wish.

#Dependencies and Options#

MusicBox depends on the following external modules/libraries for various features. Current versions that I am developing with as of this writing are:
Basics

  * ROX-Lib2 2.0.0
  * GTK+ 2.6.7 (req >= 2.4)
  * GLib 2.6.3
  * !PyGtk 2.6.1 (req >= 2.4)

Audio output (optional if your python supports ossaudiodev or linuxaudiodev, but highly recommended)

  * libao 0.8.5
  * pyao 0.82 (http://www.vorbis.com)
  * pyalsaaudio 0.2 (http://www.wilstrup.net/pyalsaaudio)

MP3 (optional, but you need at least one format supported)

  * pymad 0.4.1 (http://spacepants.org/src/pymad/)
  * libmad 0.15.1 (http://www.underbit.com/products/mad/)

ID3 tag support (Optional)

  * pyid3lib 0.5.1,
  * id3lib 3.8.3 (http://pyid3lib.sourceforge.net)

OGG (Optional)

  * pyogg 1.3,
  * pyvorbis 1.3,
  * libvorbis 1.1.0,
  * libogg 1.1.2 (http://www.vorbis.com)

FLAC (Optional)

  * libflac 1.1.2 (http://flac.sourceforge.net)
  * pyflac 0.0.1 (included, but must be built, or you can get it from most debian sites)

WAV (Standard)

  * python's built in wave module

Hopefully your distro will provide packages for these, otherwise you will have to download and build them from sources.


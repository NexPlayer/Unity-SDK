<img width="70%" text-align="center" src="./assets/logo.png" alt="NexPlayer" >

# NexPlayer  SDK for Unity

You can check our full documentation here:

https://nexplayer.github.io/Unity-SDK/

## Try our Unity Player SDK Now!

Feel free to contact us to request a demo 

* https://www.nexplayersdk.com/contact/

* support@nexplayer.com

## NexPlayer SDK for Unity Release Notes

### Version 2.3.3
- [Android]
	- [Added] Added #EXT-X-PROGRAM-DATE-TIME tag information retrieval from HLS content.
	- [Added] Multistream players events now indicate which player triggered the event.
	- [Added] New API in multistreamController for start, pause, stop, close, restart, seek all players at the same time.
	- [Added] New API in multistreamController for changing content of a player.

### Version 2.3.2
- [Unity]
    - [Fixed] Removed some NexUtility methods that shouldn't be exposed on create asset menus.
    - [Fixed] Removed .jpg files and swapped them with .png files.

- [iOS]
    - [Fixed] Fixed mute value was leeking throught scenes.
    - [Fixed] Fixed loop when changing between scenes.
    - [Fixed] Fixed overrided methods were leeking into new NexPlayer instances.
    - [Fixed] After downloading a video, regular streaming contents will still play.

- [Windows]
    - [Fixed] Fixed an error that appeared when starting the video playback.
    - [Fixed] Fixed a crash when changing or reloading the scene.
    - [Fixed] Showing multistream error with better nomenclature.
    - [Fixed] PlaybackStarted event is now thrown if starting playback from Stopped state.
    
- [macOS]
    - [Fixed] Fixed crash when releasing.
    - [Fixed] PlaybackStopped event is now only called one time.

- [WebGL]
    - [Fixed] Fixed warning on build configuration window reapearing.
    - [Fixed] Fixed an error when canceling the build.
    - [Fixed] Fixed the player looping a few frames before end of content.
    - [Fixed] PlaybackStopped event is now only called one time.
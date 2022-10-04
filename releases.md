## NexPlayer SDK for Unity Release Notes

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
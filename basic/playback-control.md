# Playback Control

The NexPlayer™ SDK provides an API that can be called to control the playback of the player.

## NexPlayer API for Playback control

Playback control methods inherited from NexPlayerBehaviour:

**public void Pause()**
This function pauses the video playback if the current state of the video playback allows it.

**public void Resume()**
This function resumes the video playback if the current state of the video playback allows it.

**public void TogglePlayPause()**
This function pauses and resumes the video playback depending on the current state of the video playback.

**public void Seek(int milliseconds)**
Seeks in the playback, moving the playback to the specified millisecond.

**public void Stop()**
This function stops the video playback and cleans the information of the current video content. 
Stopping the video will interrupt the current playback and will set the current time to 0.
To open the same content again, execute the method TogglePlayPause().

**public AsyncToken Open()**
This method initializes the media (video content) specified in the SetPreInitConfiguration() method.

**public AsyncToken Close(bool forceSync = false)**
This method ends all the work on the content currently open and terminates the SDK work. The content must be stopped before calling this method. The correct way to finish playing content is to either wait for the end of content or to call stop and wait for the stop operation to complete, then call close.

**public void ChangeVideoContent(string videoContent)**
This method closes the video content currently playing, and opens the new URL provided as a parameter.
This is not supported on WebGL. Instead, destroy the player instance, create a new instance (activated) and set a different URL in the method SetPreInitConfiguration().

**public void SetBitrate(int bitrate)**
Set the bitrate to be used and disable ABR.

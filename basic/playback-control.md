# Playback control

The NexPlayer SDK provides an API that can be called to control the playback of the player.

## NexPlayer API for Playback control

Playback control methods inherited from **NexPlayerBehaviour**:

- **public void Pause()**
    
    This function pauses the video playback if the current state of the video playback allows it.

- **public void Resume()**
    
    This function resumes the video playback if the current state of the video playback allows it.

- **public void TogglePlayPause()**

    This function pauses and resumes the video playback depending on the current state of the video playback.

- **public void Seek(int milliseconds)**
    
    Seeks in the playback, moving the playback to the specified millisecond.

- **public void Stop()**
    
    This function stops the video playback and cleans the information of the current video content. Stopping the video will interrupt the current playback and will set the current time to 0. To open the same content again, execute the method **TogglePlayPause()**.

- **public AsyncToken Open()**
    
    This method initializes the media (video content) specified in the **SetPreInitConfiguration()** method.

- **public AsyncToken Close(bool forceSync = false)**
    
    This method ends all the work on the content currently open and terminates the SDK work. The content must be stopped before calling this method. The correct way to finish playing content is to either wait for the end of content or to call stop and wait for the stop operation to complete, then call close.

- **public void ChangeVideoContent(string videoContent)**
    
    This method closes the video content currently playing, and opens the new URL provided as a parameter. This is not supported on WebGL. Instead, destroy the player instance, create a new instance (activated) and set a different URL in the method **SetPreInitConfiguration()**.

- **public void SetBitrate(int bitrate)**
    
    Set the bitrate to be used and disable ABR.

### Handling the player states
NexPlayer handles state-changing API functions asynchronously. The player’s state will not be changed immediately even if the API is called. Therefore, UI applications should check the player’s state using **getState** before calling the API. After calling any state-changing API function, UI applications must wait for the **onAsyncCmdComplete** message from the player before calling any further state-changing API functions.
NexPlayer has five possible states:

- `NEXPLAYER_STATE_NONE`
- `NEXPLAYER_STATE_CLOSED`
- `NEXPLAYER_STATE_STOP`
- `NEXPLAYER_STATE_PLAY`
- `NEXPLAYER_STATE_PAUSE`

Requests for NexPlayer to open, seek, pause, stop and resume are placed in a queue and handled in the order they are received.
When a queued operation has been completed, NexPlayer will notify the application by calling the **onAsyncCmdComplete** method in the listener.
Some of the requests can take significant time to complete (depending on various factors, for example, network conditions). Therefore, the recommended practice is for the application to issue only one request at a time and wait for that request to complete.

<!-- Playback control methods inherited from NexPlayerBehaviour:
#### Resume Command
This function resumes the video playback if the current state of the video playback allows it.
```csharp
Resume();
```
#### Pause Command
This function pauses the video playback if the current state of the video playback allows it.
```csharp
Pause();
```
#### Seek Command
Seeks in the playback, moving the playback to the specified millisecond.
```csharp
Seek(int miliseconds);
```
#### Stop Command
This function stops the video playback and cleans the information of the current video content.
Stopping the video will interrupt the current playback and will set the current time to 0.
To open the same content again, execute the method TogglePlayPause().
```csharp
Stop();
```
#### Open Command
This method initializes the media (video content) specified in the SetPreInitConfiguration() method.
```csharp
Open();
```
#### Close Command
This method ends all the work on the content currently open and terminates the SDK work. The content must be stopped before calling this method. The correct way to finish playing content is to either wait for the end of content or to call stop and wait for the stop operation to complete, then call close.
```csharp
Close();
```
#### ChangeVideoContent Command
This method closes the video content currently playing, and opens the new URL provided as a parameter.
This is not supported on WebGL. Instead, destroy the player instance, create a new instance (activated) and set a different URL in the method SetPreInitConfiguration().
```csharp
ChangeVideoContent(string NewUrl);
```
#### SetBitrate Command
Set the bitrate to be used and disable ABR.
```csharp
 SetBitrate(int bitrate);
```
### Handling the Player States
NexPlayer handles state-changing API functions asynchronously. The player’s state will not be changed immediately even if the API is called. Therefore, UI applications should check the player’s state using **getState** before calling the API. After calling any state-changing API function, UI applications must wait for the onAsyncCmdComplete message from the player before calling any further state-changing API functions.
NexPlayer has five possible states:
- `NEXPLAYER_STATE_NONE`
- `NEXPLAYER_STATE_CLOSED`
- `NEXPLAYER_STATE_STOP`
- `NEXPLAYER_STATE_PLAY`
- `NEXPLAYER_STATE_PAUSE`
- Requests for NexPlayer to open, seek, pause, stop and resume are placed in a queue and handled in the order they are received.
- When a queued operation completes, NexPlayer will notify the application by calling the **onAsyncCmdComplete** method in the listener.
- Some of the requests can take significant time to complete (depending on various factors, for example, network conditions). Therefore, the recommended practice is for the application to issue only one request at a time and wait for that request to complete. -->
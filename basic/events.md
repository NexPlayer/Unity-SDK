# Events

The NexPlayer  SDK provides a list of virtual methods which begin with "Event". These allow you to provide custom behavior to answer any **NexPlayerEvent**.

## NexPlayerAPI for events

Event triggered methods inherited from **NexPlayerBehaviour**:

- **protected virtual void EventTextureChanged()**

    Method triggered by the **NexPlayerEvent** *NEXPLAYER_EVENT_TEXTURE_CHANGED*.
    
    This event occurs whenever the reference to the internal texture has changed.

- **protected virtual void EventOnTime()**

    Method triggered by the **NexPlayerEvent** *NEXPLAYER_EVENT_TEXTURE_CHANGED*.
    
    This event occurs once per second. If the application is displaying the current play position, it should update it to reflect this new value.

- **protected virtual void EventTrackChanged()**

    Method triggered by the **NexPlayerEvent** *NEXPLAYER_EVENT_TRACK_CHANGED*.
    
    This event occurs whenever the track of the playback has changed.

- **protected virtual void EventInitComplete()**

    Method triggered by the **NexPlayerEvent** *NEXPLAYER_EVENT_INIT_COMPLETE*.
    
    This event occurs whenever the player has opened video content.

- **protected virtual void EventPlaybackStarted()**

    Method triggered by the **NexPlayerEvent** *NEXPLAYER_EVENT_PLAYBACK_STARTED*.
    
    This event occurs whenever the player has started the playback or every time it resumes the playback.

- **protected virtual void EventPlaybackPaused()**

    Method triggered by the **NexPlayerEvent** *NEXPLAYER_EVENT_PLAYBACK_PAUSED*.
    
    This event occurs whenever the player pauses the playback.

- **protected virtual void EventEndOfContent()**

    Method triggered by the **NexPlayerEvent** *NEXPLAYER_EVENT_END_OF_CONTENT*.
    
    This event occurs when the player reaches the end of the video content.

- **protected virtual void EventBufferingStarted(int percent)**

    Method triggered by the **NexPlayerEvent** *NEXPLAYER_EVENT_BUFFERING_STARTED*.
    
    This event occurs whenever the player has started buffering. Not supported on Windows and Xbox Series X/S.

- **protected virtual void EventBuffering(int percent)**
    
    Method triggered by the **NexPlayerEvent** *NEXPLAYER_EVENT_BUFFERING*.
    
    This event occurs while the player is buffering. Not supported on Windows and Xbox Series X/S.

- **protected virtual void EventBufferingEnded()**

    Method triggered by the **NexPlayerEvent** *NEXPLAYER_EVENT_BUFFERING_ENDED*.
    
    This event occurs whenever the player has finished buffering.

- **protected virtual void EventStopped()**

    Method triggered by the **NexPlayerEvent** *NEXPLAYER_EVENT_STOPPED*.
    
    This event occurs whenever the playback has stopped. Not supported on Windows and Xbox Series X/S.

- **protected virtual void EventOpened()**

    Method triggered by the **NexPlayerEvent** *NEXPLAYER_EVENT_OPENED*.
    
    This event occurs whenever the player has closed (ended all the work on the content currently open and closed content data). Not supported on Windows and Xbox Series X/S.

- **protected virtual void EventClosed()**

    Method triggered by the **NexPlayerEvent** *NEXPLAYER_EVENT_CLOSED*.
    
    This event occurs whenever the player has closed (ended all the work on the content currently open and closed content data).

- **protected virtual void EventSeeked()**

    Method triggered by the **NexPlayerEvent** *NEXPLAYER_EVENT_SEEKED*.
    
    This event occurs whenever the player has finished seeking. Not supported on Windows and Xbox Series X/S.

- **protected virtual void EventLoading()**

    Method triggered by the **NexPlayerEvent** *NEXPLAYER_EVENT_LOADING*.
    
    This event occurs whenever the player is loading.

- **protected virtual void EventTextRender()**

    Method triggered by the **NexPlayerEvent** *NEXPLAYER_EVENT_TEXT_RENDER*.
    
    This event occurs whenever playback reaches a point in time where subtitles on any track need to be displayed or cleared.

- **protected virtual void EventTextInit()**

    Method triggered by the **NexPlayerEvent** *NEXPLAYER_EVENT_TEXT_INIT*.
    
    This event occurs when the subtitle parsing is complete. Not supported on Windows and Xbox Series X/S.

- **protected virtual void EventTimedMetadataRender()**

    Method triggered by the **NexPlayerEvent** *NEXPLAYER_EVENT_TIMED_METADATA_RENDER*.
    
    This event occurs when new timed metadata is ready for display in HLS. Timed metadata includes additional information about the playing content that may be displayed to the user, and this information may change at different times throughout the content. Each time new metadata is available for display, this event is triggered.

- **protected virtual void EventTotalTimeChanged()**

    Method triggered by the **NexPlayerEvent** *NEXPLAYER_EVENT_ON_TOTAL_TIME_CHANGED*.
    
    This event occurs when the total time changes during the playback. Normally it's triggered when the end of the seekable range loads further during a live stream.

- **protected virtual void EventHandleAudioPCM(int ts, float[] buff)**

    Method triggered by the **NexPlayerEvent** *NEXPLAYER_EVENT_ON_HANDLE_EXTERNAL_PCM*.
    
    This event occurs whenever there is new audio PCM data during the playback. The audio buffers are floats ranging from -1.0f to 1.0f. Supported on Android, Windows, and Xbox Series X/S.

- **protected virtual void EventUnhandled()**

    Unhandled event case.
    
    This is called when the event was not handled by other methods.

- **protected virtual void Error(NexErrorCode error)**

    Method triggered by the **NexPlayerEvent** *NEXPLAYER_EVENT_ERROR*.
    
    This event is triggered when an internal error occurs. The base implementation of this method logs the error information and calls the error specific virtual function. On Windows and Xbox Series X/S it only supports the **NexErrorCodes** *PLAYER_ERROR_TIME_LOCKED*, *HAS_NO_EFFECT* and *ERROR_MEDIA_NOT_FOUND*.


## Sample code for events

The following sample code shows how to override inherited virtual methods to respond to any NexPlayer  event:

```csharp
public class NexPlayerSimple : NexPlayerBehaviour
{
    protected override void SetPreInitConfiguration()
    {
        base.SetPreInitConfiguration();

        // run any custom code
    }
}

```
You will find the usage of this API in the code of our sample project located at **Packages > NexPlayer Simple Sample (com.nexplayer.nxplayersimplesample) > NexPlayer > SampleCode > Players > NexPlayerSimple.cs**.
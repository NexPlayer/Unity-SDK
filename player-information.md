# Player information

## NexPlayer API for player information

Player information methods inherited from NexPlayerBehaviour:

**public NexPlayerStatus GetPlayerStatus()**
Retrieves the current state of the player.

**public int GetCurrentTime()**
For VOD streams, it retrieves the current playback time. 
For live streams, Android, iOS, macOS, and WebGL, the current time is the current PTS value of the audio track while, on Windows and Xbox Series X/S, it is the server time value and this value only updates once per second.

**public int GetTotalTime()**
For VOD streams, it retrieves the media duration of the current content. 
For live streams on Android and Windows and Xbox Series X/S, the end of the range of the current content that is seekable when the isLiveStream property is enabled. Additionally, this function will trigger the event NEXPLAYER_EVENT_ON_TOTAL_TIME_CHANGED whenever the maximum seekable range is updated.

**public NexRenderMode GetRenderMode()**
Retrieves the current render mode the player is using.

## Sample code for player information

The player info can be obtained from any script, but in the following example it’s done on every frame. For this, override the Update method and call the base implementation. Then, you can retrieve information about the player by using API methods such as GetPlayerStatus(), GetCurrentTime(), GetTotalTime() and GetRenderMode();

```csharp
// Override EventOnTime to execute the following code once per second.
// This is useful for UI.
protected override void EventOnTime()
{
      base.EventOnTime();

      NexPlayerStatus currentStatus = GetPlayerStatus();
      int currentTime = GetCurrentTime();
      int totalTime = GetTotalTime();

      NexRenderMode currentMode = GetRenderMode();
}
```

You will find the usage of this API in the code of our sample project located at Packages → NexPlayer Simple Sample → NexPlayer → SampleCode → Players → NexPlayerSimple.cs (in Finder: Packages/com.nexplayer.nxplayersimplesample/NexPlayer/SampleCode/Players/NexPlayerSimple.cs) by unfolding the “Player information” region.
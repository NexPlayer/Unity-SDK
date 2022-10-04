# Audio tracks

The NexPlayer™ SDK provides the functionality to retrieve and select the Audio Tracks configured in any DASH and HLS manifest. For example, to output and change the audio from English to Spanish. This functionality is only supported on Android and iOS devices.

## NexPlayer™ API for audio tracks

#### Audio track variables inherited from NexPlayerBehaviour

**public struct NexPlayerAudioStream**
Struct to store information of one audio track. It contains:

- **public int id:** ID of the audio track.
- **public string name:** Name of the audio track if available (NAME Tag in The Manifest).
- **public string language:** Language of the audio track if available  (LANGUAGE Tag in The Manifest).

#### Audio track methods inherited from NexPlayerBehaviour

**public NexPlayerAudioStream[] GetAudioStreamList()**
Returns an array of all the possible audio tracks or null if the platform doesn't support it.

**public virtual void SetAudioStream(NexPlayerAudioStream audioStream)**
Sets a track to be used during the video playback. The list of possible audio tracks can be obtained with the method GetAudioStreams.

## Sample code for audio tracks

In order to control which audio track is playing and change it in your custom player, the first step is to create a variable to save all the audio tracks extracted from the manifest. In order to be sure that the manifest has been read, you should override the virtual function EventPlaybackStarted:

```csharp
// variable for storing the information about the audio tracks present inside the manifest
NexPlayerAudioStream[] audioStreams;

protected override void EventPlaybackStarted()
{
    base.EventPlaybackStarted();
    // At this event the player has finished reading the manifest and is safe to ask for the audio tracks
    audioStreams = GetAudioStreamList();
}
```
Finally, create a public method to change the current audio track at runtime:

```csharp
public void SetAudioStream(int index)
{
    if (audioStreams == null)
    {
        Log("Audio Streams is null");
        return;
    }

    if (index < 0 || index >= audioStreams.Length)
    {
        Log($"Requested index: {index}, is out of bounds");
        return;
    }

    SetAudioStream(audioStreams[index]);
}
```

You will find the usage of this API in the code of our sample project located at **Packages > NexPlayer™ Simple Sample (com.nexplayer.nxplayersimplesample) > NexPlayer > SampleCode > Players > NexPlayerMultipleLanguages.cs**.
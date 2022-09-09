# Closed captions

The NexPlayer™ SDK supports retrieval, selection and display of closed captions configured in any DASH and HLS manifest. For example, to change the captions from English to Spanish and display them. This functionality is only supported in Android and iOS devices.

# NexPlayer API for closed captions

#### Closed captions variables inherited from NexPlayerBehaviour:

**public struct NexSubtitleElement**
Struct to store all the information related to one subtitle element (one string text that must be outputted at a given playback time). The information stored is:

- **public string caption:** Subtitle data string to be outputted.
- **public int startTime:** Start time in milliseconds when the caption starts to show.
- **public int endTime:** End time in milliseconds when the caption stops being shown.
- **public string encodingType:** Caption encoding type (utf-8, utf-16, utf-16BE, euc-kr, etc..).
- **public NexPlayer_Caption_Type captionType:** The caption type, a helper enum for utilities.
- **public struct NexPlayerCaptionStream:** Struct to store one audio track’s information. It contains:
- **public int id:** ID of the closed caption track (ID Tag in The Manifest).
- **public string name:** Name of the closed caption track if available (NAME Tag in The Manifest).
- **public string language:** Language of the closed caption track if available  (LANGUAGE Tag in The Manifest).

**Closed captions methods inherited from NexPlayerBehaviour:**

**public virtual NexSubtitleElement GetCurrentSubtitleElement()**
Returns the current subtitle information.

**public virtual NexPlayerCaptionStream[] GetCaptionStreamList()**
Returns an array of all the possible closed caption tracks or null if the platform doesn't support it.

**public virtual void SetAudioStream(NexPlayerAudioStream audioStream)**
Sets a closed caption track to be used during the video playback. The possible closed caption tracks can be obtained from the method GetCaptionStreamList.

#### Sample code for closed captions

**public void SetWidevineHeaders(string[] keys, string[] values)**
Optionally, NexPlayer allows sending headers within the license server request, in case they are needed to get the license key(s). It takes two string arrays, the first one contains the keys and the second the values. Both arrays must have the same size and key in position (i) must pair with the value in the same (i) position.

**public void ClearWidevineHeaders()**
Clear all the widevine headers and keys.

**public bool UpdateWidevineHeaderValue(string key, string value)**
Changes the value assigned to the given key to the given value. Returns true if the key is found and successfully set.


# Sample code for playing Widevine content:

Similar to the audio tracks, in order to control which closed caption track will be outputted by the player, it is necessary to declare a variable of type NexPlayerCaptionStream to store the information extracted from the manifest. This information is retrieved after the event EventPlaybackStarted. Also, create a public method for setting the desired closed caption track:

```csharp
// variable for storing the information about the closed captions tracks present inside the manifest
NexPlayerCaptionStream[] captionStreams;

protected override void EventPlaybackStarted()
{
    base.EventPlaybackStarted();

    // At this event the player has finished reading the manifest and is safe to ask for the CC tracks
    captionStreams = GetCaptionStreamList();
}

public void SetCaptionStream(int index)
{
    if (captionStreams == null)
    {
        Log("Caption Streams is null");
        return;
    }

    if (index < 0 || index >= captionStreams.Length)
    {
        Log($"Requested index: {index}, is out of bounds");
        return;
    }

    SetCaptionStream(captionStreams[index]);
}
```
In order to render the captions during the playback, use the struct NexSubtitleElement and override the function EventTextRender:

```csharp
// variable for holding one subtitle element at a time
NexSubtitleElement subtitleElement;

protected override void EventTextRender()
{
    base.EventTextRender();
    // get information about the string that must be shown 
    subtitleElement = GetCurrentSubtitleElement();
    if (subtitleElement.caption != null)
    {
        // show the string by assigning it to a Unity UI text element
        captionLabel.text = subtitleElement.caption;
    }
}
```

You will find the usage of this API in the code of our sample project located at Packages → NexPlayer Simple Sample → NexPlayer → SampleCode → Players → NexPlayerMultipleLanguage.cs (in Finder: Packages/com.nexplayer.nxplayersimplesample/NexPlayer/SampleCode/Players/NexPlayerMultipleLanguages.cs).
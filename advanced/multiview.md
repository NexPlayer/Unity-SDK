# MultiView

***This is a premium feature***

Multiview is only supported on iOS.

NexPlayer MultiView feature provides a way to reproduce up to 8 simultaneous streams on the same scene. This streams might use the same properties as the ones abailables for single stream.

---
## NexPlayer API for Multiview

When using multiview on your project you should use the ***MultistreamController*** field provided by **NexPlayerBehaviour**.

The specific API provided by this controller to manage multiview is the following.

##### Init(NexPlayerBehaviour nexPlayerBehaviour)
Initialization for MultistreamController. It uses the NexPlayerBehaviour to play the videos.

##### SetMultiStreamRender()
This method will automatically set the render mode for multiview. It will check first for RawImages and after for RenderTextures. You should only initialize the List for render mode that you are going to use.

##### ChooseControlIndex(int index)
Select a player instance to control.

### Playback Control

##### StartAllPlayers()
Open the content for all multiview instances and sets them ready to play.

##### StartChosenPlayer()
Open the content for selected player instance using the *multiURLPaths* list field as content . Use method *ChooseControlIndex(int index)* to decide which instance is selected.

##### StartVideo(string url)
Starts the selected player instance with an specific content.

##### ResumeAllPlayers()
Resumes the playback of all multiview instances.

##### PauseAllPlayers()
Pauses the playback of all multiview instances.

##### StopAllPlayers()
Pauses the playback of all multiview instances and sets them on stop state. Stop will pause the playback and set the playback time to 0ms.

##### CloseAllPlayers()
Closes the playback of all multiview instances.

##### ReleaseAllPlayers()
Release the playback of all multiview instances. It also release and destroy *MultistreamController* instance.

##### RestartMultiStreamsPlayback()
Restart the playback of all multiview instances to the beggining of the content.

### OTHERS

##### ChangeVideoContent(string url)
Change the content of the selected player instance. The content can be changed on run time. Internally this method close the chosen player, sets the new stream url and start the new content from the beggining.

##### GetMultiStreamNumber()
Returns the number of streams applied to the ***MultistreamController***.

##### MultiStreamSetProperties()
Sets the specific properties such as ABR and SPD to multiview streams. You should set the value for this properties before calling this method, such as:  
> NexPlayerBehaviour.SynchronizationEnable = true;

##### SetMuteMultiStreams(bool setMuted)
Mute or unmute all multiview players.

##### MultiStreamHTTPHeaders(int playerIndex, string key, string value)
Adds a HTTP header to the *playerIndex* player with *key* and *value*.

##### SetMultiStreamsBitrate(int bitrate)
This method allow setting the bitrate of all streams. Bitrate value should be in bits.

---
## Sample code for Multiview

This sample will only use code to setup de environment and will use RawImages to render. You can also use the Unity editor to speed up some steps.

Like all custom players, inherit from **NexPlayerBehaviour**, use field **NexPlayerMultistreamController** provided by NexPlayerBehaviour to allow for multiple streams and **NexPlayerRenderController** to display the videos on Unity objects.

```csharp
public class NexPlayerMultistream : NexPlayerBehaviour {
    private NexPlayerRenderController renderController;

    private List<RawImage> rawImages; 
    private NexRenderMode renderMode = NexRenderMode.RawImage;
```

Lets override the Monobehaviour method Awake() to initialize the required components.

```csharp
protected override void Awake()
    {
        // Render Controller
        renderController = gameObject.AddComponent<NexPlayerRenderController>();

        // MultistreamController field provided by NexPlayerBehaviour
        MultistreamController = gameObject.AddComponent<NexPlayerMultistreamController>();

        if (renderMode == NexRenderMode.RawImage) {
            // By default video will appear inverted, that's why we use Rotate()
            rawImages = new List<RawImage>();
            RawImage raw = GameObject.Find("RawImage0").GetComponent<RawImage>();
            raw.transform.Rotate(180.0f, 0.0f, 0.0f, Space.Self);
            rawImages.Add(raw);
            raw = GameObject.Find("RawImage1").GetComponent<RawImage>();
            raw.transform.Rotate(180.0f, 0.0f, 0.0f, Space.Self);
            rawImages.Add(raw);

            MultistreamController.multiRawImages = rawImages;
        }

        //debugLogs = true;

        base.Awake();
    }
```

Now lets override method **InitControllers** to do the final initialization of our controllers.

```csharp
protected override void InitControllers()
    {
        base.InitControllers();

        // Streams
        MultistreamController.numberOfStreams = 2;
        List<string> urls = new List<string>();
        urls.Add("https://bitdash-a.akamaihd.net/content/MI201109210084_1/m3u8s/f08e80da-bf1d-4e3d-8899-f0f6155f6efa.m3u8");
        urls.Add("https://s3.eu-west-3.amazonaws.com/content.nexplayersdk.com/hls/BustiContent/Race1/master.m3u8");
        MultistreamController.multiURLPaths = urls;
        MultistreamController.Init(this);

        // RenderController
        renderController.StartingRenderMode = renderMode;
        renderController.Init(this);
    }
```

Then, lets override the **SetPreInitConfiguration** method, here you should set your playback settings, so this settings are applyed before the player is opened:

```csharp
protected override void SetPreInitConfiguration() {
	base.SetPreInitConfiguration();

    autoPlay = true;
    loop = true;
    mutePlay = false;
    volume = 0.5f;
}
```

There are lots of functions for events you can override to do the custom actions you desire whenever one stream trigguers an event. You don't need to call the base."overridenEvent" for this functions.  
Keep in mind there are 2 kinds of functions for events, the ones with a parameter wich indicates the player instance that triggered the event and another one for only 1 stream (without playerInstance parameter).

Here are a couple of examples of multiview event functions:

```csharp
protected override void EventStopped(int playerInstance) {
	Debug.Log("Stopped for instance - " + playerInstance);
}

protected override void EventEndOfContent(int playerInstance)
{
	Debug.Log("EndOfContent for instance - " + playerInstance);
}

protected override void EventPlaybackStarted(int playerInstance)  
{
	Debug.Log("PlaybackStarted for instance - " + playerInstance);
}

protected override void EventPlaybackStarted() {
	Debug.Log("This event will never be trigguered when using multiview");
}
```

About the track change, there is a function to alternate which Multiview instance plays at the highest bitrate and which one(s) at the lowest.

```csharp
public void Swap()  
{  
   // Only load the maximum and minimum bitrate once  
   if(minBitrate == 0|| maxBitrate == 0)  
   {  
       minBitrate = GetMinBitrate();  
       maxBitrate = GetMaxBitrate();  
   }  
  
   mainScreenIndex = (mainScreenIndex + 1) % MultistreamController.GetMultiStreamNumber();  
  
   ForceBitRate(mainScreenIndex, maxBitrate);  
}
```

The method ForceBitRate changes the streams’ resolutions, regarding the Multiview instance player and the target bitrate.

```csharp
private void ForceBitRate(intindex, int bitrate)  
{  
   // Choose player index to control  
   MultistreamController.ChooseControlIndex(index);
  
   // Set bandwidth to specific tracks' bitrate  
   SetMaxAndTargetBitrate(bitrate);  
}
```

Whenever you want to apply a specific method property to all players, simplest way to do it is the following:

```csharp
// Pitch feature is only available for iOS and Android devices.
public void setPitchAllPlayers(int value) {
	for (int i = 0; i < MultistreamController.GetMultiStreamNumber(); i++) {
		MultistreamController.ChooseControlIndex(i);
		SetPitch(value);
	}
}
```

You will find the usage of this API in the code of our sample project located at Packages → NexPlayer Simple Sample → NexPlayer → SampleCode → Players → NexPlayerMultiview.cs (in Finder: Packages/com.nexplayer.nxplayersimplesample/NexPlayer/SampleCode/Players/NexPlayerMultiview.cs).
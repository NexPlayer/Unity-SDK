# MultiView

NexPlayer MultiView feature provides a way to reproduce up to 8 simultaneous streams on the same scene. This streams might use the same properties as the ones abailables for single stream.

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

Now lets override method **InitControllers** to do the final initialization of our controllers. You can add more stream urls if desired.

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


Then, lets override the **SetPreInitConfiguration** method, making sure to call the base implementation, to set your playback settings before the player is opened:

```csharp
protected override void SetPreInitConfiguration() {
	base.SetPreInitConfiguration();

    autoPlay = true;
    loop = true;
    mutePlay = false;
    volume = 0.5f;
}
```
There are lots of functions for events you can override to do the custom actions you desire whenever one stream trigguer the event.  
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
```
About the track change, we have implemented a function to alternate which Multiview instance plays at the highest bitrate and which one(s) at the lowest.

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

## NexPlayer API for Multiview

When using multiview on your project you should use the MultistreamController field provided by NexPlayerBehaviour.

The specific API provided by this controller to manage multistream is the following.


TALK ABOUT API

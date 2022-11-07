# Multiview

This is a premium feature. To find out more information, please contact NexPlayer's Unity Team at unity.support@nexplayer.com

NexPlayer's Multiview feature provides a way to reproduce up to 8 simultaneous streams in the same scene. These streams might use the same properties as the ones available for a single stream.

## NexPlayer  API for Multiview

When using Multiview on your project you should use the **MultistreamController** field provided by **NexPlayerBehaviour**.

The specific API provided by this controller to manage Multiview is the following:

- **Init(NexPlayerBehaviour nexPlayerBehaviour)**
    - Initialization for **MultistreamController**. It uses the **NexPlayerBehaviour** to play the videos.

- **SetMultiStreamRender()**
    - This method will automatically set the render mode for Multiview. It will check for RawImages first and then for RenderTextures. You should only initialize the List for the render mode that you're going to use.

- **ChooseControlIndex(int index)**
    - Selects a player instance to control.

### Playback Control

- **StartAllPlayers()**
    - Opens the content for all Multiview instances and sets them ready to play.

- **StartChosenPlayer()**
    - Opens the content for selected player instance using the **multiURLPaths** list field as content. Use method **ChooseControlIndex(int index)** to decide which instance is selected.

- **StartVideo(string url)**
    - Starts the selected player instance with a specific content.

- **ResumeAllPlayers()**
    - Resume the playback of all contents.

- **PauseAllPlayers()**
    - Pauses the playback of all contents.

- **StopAllPlayers()**
    - Stop the playback of all videos and sets the time for them at the beggining of the content.

- **CloseAllPlayers()**
    - Stop playback & closes all players handled by multistreamController.

- **ReleaseAllPlayers()**
    - Release & close all info for all players handled by multistreamController.

- **RestartMultiStreamsPlayback()**
    - Restart the playback of all Multiview instances to the beginning of the content.

### Properties

- **MultiStreamSetProperties()**
	- Sets the specific properties such as ABR and SPD to Multiview streams. You should set the value for these properties before calling this method, such as:  
    
    > NexPlayerBehaviour.SynchronizationEnable = true;

- **SetMuteMultiStreams(bool setMuted)**
   - Mute or unmute all Multiview players.

- **SetMultiStreamsBitrate(int bitrate)**
	- Sets the bitrate targeted for all players. Bitrate value should be in bits.

- **SetHTTPHeader(int playerIndex, string key, string value)**
	- Adds a new HTTP header to the **playerIndex** player with **key** and **value**.

### Other functions

- **ChangeVideoContent(string url)**
    - Change the content of the selected player instance. The content can be changed during runtime. Internally, this method closes the chosen player, sets the new stream URL and starts the new content from the beginning.

- **GetMultiStreamNumber()**
    - Returns the number of streams applied to the **MultistreamController**.

- **AllPlayersAreReady()**
	 - Returns a boolean value that indicates whether all players are ready to start playing.

## Sample code for Multiview

This sample will only use code to setup the environment and will use RawImages to render. You can also use the Unity editor to speed up some steps.

Like all custom players, inherited from **NexPlayerBehaviour**, use the field **NexPlayerMultistreamController** provided by **NexPlayerBehaviour** to allow for multiple streams and **NexPlayerRenderController** to display the videos on Unity objects.

```csharp
public class NexPlayerMultistream : NexPlayerBehaviour {
    private NexPlayerRenderController renderController;

    private List<RawImage> rawImages; 
    private NexRenderMode renderMode = NexRenderMode.RawImage;
```

Let's override the **MonoBehaviour** method **Awake()** to initialize the required components:

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

Now, let's override method **InitControllers** to do the final initialization of our controllers:

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

Then, override the **SetPreInitConfiguration** method. Here you should set your playback settings, so these settings are applied before the player is opened:

```csharp
protected override void SetPreInitConfiguration() {
	base.SetPreInitConfiguration();

    autoPlay = true;
    loop = true;
    mutePlay = false;
    volume = 0.5f;
}
```

Regarding changing tracks, there is a function to determine which Multiview instance plays at the highest bitrate and which ones are lowest:

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

The method **ForceBitRate** changes the streams' resolutions, defining the Multiview instance player and the target bitrate:

```csharp
private void ForceBitRate(int index, int bitrate)  
{  
   // Choose player index to control  
   MultistreamController.ChooseControlIndex(index);
  
   // Set bandwidth to specific tracks' bitrate  
   SetMaxAndTargetBitrate(bitrate);  
}
```

Whenever you want to apply a specific method property to all players, the simplest way to do so can be seen below:

```csharp
public void Resume() {
	for (int i = 0; i < MultistreamController.GetMultiStreamNumber(); i++) {
		MultistreamController.ChooseControlIndex(i);
		Resume();
	}
}
```

You will find the usage of this API in the code of our sample project located at **Packages > NexPlayer Simple Sample (com.nexplayer.nxplayersimplesample) > NexPlayer > SampleCode > Players > NexPlayerMultiview.cs**.

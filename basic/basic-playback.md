# Basic Playback

NexPlayer™ plays non-DRM (HLS, DASH or MP4) content by simply providing a valid URL and configuring the rendering.

## NexPlayer™ API for Basic Playback

Basic variables inherited from NexPlayerBehavior:

- **public string URL**
URL to get the media from.

- **public bool isLiveStream**
Enable when the video to be opened is a live stream. Takes effect when Open() is called.This setting will make the GetTotalTime() function to retrieve the maximum seekable range of the current content. This setting only works on Android and Windows platforms.

- **public bool autoPlay**
When enabled the video will auto start playing. Otherwise the video will be initialized, but the playback will not start automatically, remaining paused.

- **public bool loopPlay**
When enabled the player will restart the playback from the beginning when it reaches the end of the video content.

- **public bool mutePlay**
When enabled the player will be muted. When disabled, the player will use volume.

- **public float volume**
Sets the volume of the player (0 - 1).

Basic methods inherited from NexPlayerBehaviour:

**protected virtual void InitControllers()**  
Method called prior to the player creation. Use it to initialize all the controllers needed for the custom player.

**protected virtual void SetPreInitConfiguration()**  
Method called prior to the player creation. Use it to initialize all the variables needed for the basic playback settings such as URL, isLiveStream, autoplay, volume, etc...

```chsarp
protected override void SetPreInitConfiguration() {
	base.SetPreInitConfiguration();
	
	URL = "testUrl";
	isLiveStream = false;
	
	// After opening the content the player will automatically start playing.
	autoPlay = true;
	// The player will stop when it reaches the end of the content.
	loopPlay = false;
	// The player will start with sound enabled.
	mutePlay = false;
	// The player starts with maximum volume.
	volume = 1;
}
```

## Sample code for Basic Playback (non-DRM):

The code needs to inherit from NexPlayerBehaviour and requires the NexPlayerRendererController: The render controller must be set according to the scene’s needs. Configure the startingRenderMode and the target render object accordingly:

```csharp
[RequireComponent(typeof(NexPlayerRenderController))]
public class NexPlayerSimple : NexPlayerBehaviour
{
  private NexPlayerRenderController renderController;

  protected override void InitControllers()
  {
      base.InitControllers();

      renderController = GetComponent<NexPlayerRenderController>();

      NexRenderMode targetRenderMode = NexRenderMode.RawImage; // Change the sample's render mode

      switch (targetRenderMode)
      {
          case NexRenderMode.RawImage:
              // one of many ways to obtain a reference to the desired Raw Image
              RawImage targetRawImage = FindObjectOfType<RawImage>();
              // Set the target Raw Image
              renderController.rawImage = targetRawImage;
              // Set render mode to Raw Image
              renderController.StartingRenderMode = NexRenderMode.RawImage;
              break;
          case NexRenderMode.RenderTexture:
              // one of many ways to obtain a reference to the desired Render Texture
              RenderTexture targetRenderTexture = Resources.Load<RenderTexture>("PathToAssetInsideResources");
              // Set the target Render Texture
              renderController.renderTexture = targetRenderTexture;
              // Set render mode to Render Texture
              renderController.StartingRenderMode = NexRenderMode.RenderTexture;
              break;
          case NexRenderMode.MaterialOverride:
              // one of many ways to obtain a reference to the desired Material Override
              Renderer targetMaterialOverride = FindObjectOfType<Renderer>();
              // Set the target Material Override
              renderController.materialOverride = targetMaterialOverride;
              // Set render mode to Material Override
              renderController.StartingRenderMode = NexRenderMode.MaterialOverride;
              break;
          default:
              break;
      }

      renderController.Init(this);
  }
```

You will find the usage of this API in the code of our sample project located at Packages → NexPlayer™ Simple Sample → NexPlayer™ → SampleCode → Players → NexPlayerSimple.cs (in Finder: Packages/com.nexplayer.nxplayersimplesample/NexPlayer/SampleCode/Players/NexPlayerSimple.cs) by unfolding the “Render Mode” region.
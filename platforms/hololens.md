# Hololens

## Detailed feature list
#### Media Source
- Streams (*External URL*)
	- HLS (.m3u8)
	- DASH (.mpd)
	- MP4 (.mp4)
- AssetPlay (*Streaming Assets folder*)
	- MP4 (.mp4)
	- AVI (.avi)
	- MKV (.mkv)
- Local Play (*Any local folder*)
	- MP4 (.mp4)
	- AVI (.avi)
	- MKV (.mkv)

#### Rendering Mode  
- RawImage (*Unity UI*)	
- RenderTexture (*Unity Asset*)
- Material Override (*Material's MainTexture*)

#### Sound Playback Control
- Volume Control
- Mute Volume

#### Video Playback Control
- Start Player
- Pause Media
- Resume Media
- Stop Media
- Close Player
- Seek
- AutoPlay
- Loop
- Maximize Screen
- Run In Background

#### Miscellaneous
- 360 Media Playback
- Video with transparency (*Chroma Shader*)
- Video Spread (*World Space Shader*)
- Play Video on multiple objects

#### Audio Codecs
- AAC-LC 

#### Video Codecs
- H.264
- MPEG-4

## Build Configuration

**Build Settings → Switch Platform** to Universal Windows Platform, and follow below configuration:

![](../assets/platforms/holo8.png)

**Player Settings → Player → Other Settings → Capabilities → Script Compilation → Add UWP macro**:

![](../assets/platforms/holo9.png)

Go to **Player Settings → Player → Publishing Settings → Capabilities** and check the **InternetClient** checkbox in order to allow our SDK to access the internet:

![](../assets/platforms/holo10.png)

Change the Plugin setting to target **UWP** and set **CPU** to **ARM64** in the Inspector:

![](../assets/platforms/holo11.png)

Create a folder in the project directory where builds will be saved, then navigate to **Build Settings → Build** and select the build folder:

![](../assets/platforms/holo12.png)

This will generate new Visual Studio solution inside the build folder. Open the .sln file:

![](../assets/platforms/holo13.png)

### UWP Hololens 2 Deployment

- Open the the startup project's **Properties**
- Change Platform to **ARM64**
- Deploy using your preferred method (**Remote Machine**, **Emulator**)

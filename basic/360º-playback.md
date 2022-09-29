# 360° playback

NexPlayer™ has support for 360° video. This feature doesn’t require any specific API or code, as it’s entirely implemented in the Unity Editor. 

## Scene setup

To configure a scene for 360° video, use the simple player configured for Material Override rendering. Then, place the camera inside of a Sphere, where the video will be rendered.
Next, add the script *Packages/com.nexplayer.nxplayerfullfeatsample/NexPlayer/SampleCode/FullFeat/UI/StereoMode.cs* to the Sphere game object and set the projection mode to match the content. Finally, to handle the camera rotation, add the script *NexPlayer360Controller.cs* to the video player GameObject and set the camera reference.
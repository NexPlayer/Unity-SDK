# Reduce the Build File Size

Application Stores for Android and iOS have a limited file size to distribute the app.
The NexPlayer™ Unity SDK can be reduced to occupy the minimum size possible.

It’s recommended to follow the next steps to optimize the Unity SDK:

## Android

- **Check the Unity option for Build App Bundle whenever possible.**
This option will make a selective apk creation, depending on the different mobile device platforms and will not include unnecessary plugin files in the apk. Also set the compression method to **LZ4HC**.

![](../assets/platforms/red1.png)

- **Remove all the unnecessary .so libraries that the Player will not need.** They are located under:
	- Packages/com.nexplayer.nxplayersdk/NexPlayer/Plugins/Android/libs/arm64-v8a.
	- Packages/com.nexplayer.nxplayersdk/NexPlayer/Plugins/Android/libs/armeabi-v7a.

- **Libnexplayerengine_vm.so, libnexcal_dolby_armv7.so and every sample .so** can be deleted without affecting the Player’s behaviour.

- Make sure to set Player Settings → Other Settings → Configuration → **Api Compatibility Level** to **.NET Standard 2.0** option and **Scripting Backend** to **IL2CPP**.

![](../assets/platforms/red2.png)

- Set Player settings → Other settings → Optimization → **Managed Stripping** level to **high. You may need to adjust this if you have runtime issues.**

![](../assets/platforms/red3.png)

## iOS

- Set the Player Settings → Other Settings → Optimization → **Managed Stripping Level** to **high**, Player Settings → Other Settings → Optimization → **Script Call Optimization** to **Fast but no Exceptions** and make sure to check Player Settings → Other Settings → Optimization → **Strip Engine Code**.

![](../assets/platforms/red4.png)

- Set the Build Settings’ compression method to **LZ4HC**.

![](../assets/platforms/red5.png)
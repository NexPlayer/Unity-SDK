# Synchronization

***This is a premium feature***

Synchronization is only supported on iOS and Android.

NexPlayer synchronization technology allows you to sync the video arrival and stream video synchronously across different devices using the DASH SPD value. This is also possible for HLS streams by controlling the SPD value from the client-side.

## NexPlayer API for synchronization

#### Synchronization variables inherited from NexPlayerBehavior:

**public bool SynchronizationEnable**
Enables or disables the use of synchronization to UTC time (SPD).

**public uint DelayTime**
Presentation delay to synchronize end users, it sets a latency between the original stream and the player’s arrival.

**public uint SpeedUpSyncTime**
Maximum time that the playback is allowed to be out of synchronization before it changes playback speed to get synchronized again with the latency set in the Delay Time.

**public uint JumpSyncTime**
Maximum time that the playback is allowed to be out of synchronization before it jumps to synchronize the video with the latency set in the Delay Time.

#### Sample code for synchronization

**public void SetWidevineHeaders(string[] keys, string[] values)**
Optionally, NexPlayer allows sending headers within the license server request, in case they are needed to get the license key(s). It takes two string arrays, the first one contains the keys and the second the values. Both arrays must have the same size and key in position (i) must pair with the value in the same (i) position.

**public void ClearWidevineHeaders()**
Clear all the widevine headers and keys.

**public bool UpdateWidevineHeaderValue(string key, string value)**
Changes the value assigned to the given key to the given value. Returns true if the key is found and successfully set.


## Sample code for playing Widevine content:

Synchronization technology (SPD) is meant to be used with live streaming content only. After setting a live content URL just set the synchronization variables inherited from NexPlayerBehaviour, and synchronization technology will automatically be triggered. The variables must be set prior to the player initialization, so use the method SetPreInitConfiguration to do so:


```csharp
protected override void SetPreInitConfiguration()
{
    base.SetPreInitConfiguration();

    URL = "yourlivecontentURL";

    // enable Synchronization functionality
    SynchronizationEnable = true;

    // set the presentation delay to one second
    DelayTime = 1000;

    // set the max time out of synchronization to trigger speed up
    SpeedUpSyncTime = 500;

    // set the max time out of synchronization to trigger seeking
    JumpSyncTime = 1000;
}
```
You will find the usage of this API in the code of our sample project located at Packages → NexPlayer Simple Sample → NexPlayer → SampleCode → Players → NexPlayerSimple.cs (in Finder: Packages/com.nexplayer.nxplayersimplesample/NexPlayer/SampleCode/Players/NexPlayerSimple.cs) by unfolding the “Synchronization” region.
# NexPlayer  logs

NexPlayer has support for allowing and prohibiting the displaying descriptive debugging logs. When enabled, the procedure to see these logs is different per platform. You can find more information at the following link:
[https://docs.unity3d.com/Manual/LogFiles.html](https://docs.unity3d.com/Manual/LogFiles.html)

## NexPlayer  API for logs

Logs and information variables inherited from **NexPlayerBehaviour**:

- **public bool debugLogs**
    
    Enables printing NexPlayer  information logs in the debug console.

## Sample code for logs

The API for logs must be set before opening the player, NexPlayer  provides the virtual method **SetPreInitConfiguration()** to do so:

```csharp
protected override void SetPreInitConfiguration()
{
    base.SetPreInitConfiguration();
    ...
    debugLogs = true;  // enabling debug logs
    ...
}
```

You will find the usage of this API in the code of our sample project located at **Packages > NexPlayer  Simple Sample (com.nexplayer.nxplayersimplesample) > NexPlayer > SampleCode > Players > NexPlayerSimple.cs** by unfolding the "Debug" region.
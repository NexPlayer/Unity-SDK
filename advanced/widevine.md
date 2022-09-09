# WideVine

***This is a premium feature***

WideVine is only supported on iOS and Android.

NexPlayer provides the integration for Widevine encrypted content right out of the box, by inheriting from NexPlayerBehaviour.

# NexPlayer API for Widevine

#### Widevine variables inherited from NexPlayerBehaviour:

**public string keyServerURI**
Endpoint server, which is responsible for managing and storing the key that will be used for decrypting the content segments.

**public uint licenseRequestTimeout**
The maximum time in seconds the player waits for the server response before returning a timeout error message. Zero means no timeout.

#### Widevine methods inherited from NexPlayerBehaviour:

**public void SetWidevineHeaders(string[] keys, string[] values)**
Optionally, NexPlayer allows sending headers within the license server request, in case they are needed to get the license key(s). It takes two string arrays, the first one contains the keys and the second the values. Both arrays must have the same size and key in position (i) must pair with the value in the same (i) position.

**public void ClearWidevineHeaders()**
Clear all the widevine headers and keys.

**public bool UpdateWidevineHeaderValue(string key, string value)**
Changes the value assigned to the given key to the given value. Returns true if the key is found and successfully set.


# Sample code for playing Widevine content:

All widevine settings must be set before opening the player, NexPlayer provides the virtual method SetPreInitConfiguration() to do so:


```csharp
protected override void SetPreInitConfiguration()
{
    base.SetPreInitConfiguration();
    ... 
    #region Widevine Playback
    // mandatory Widevine encrypted content
    keyServerURI = "your key server url";
    licenseRequestTimeout = 0;            // optional

    // Only when using additional widevine headers
    string[] wvHeaderKeys = new string[] { "key1",  "key2"};
    string[] wvheaderValues = new string[] { "value1",  "value2"};
    SetWidevineHeaders(wvHeaderKeys, wvheaderValues);
    #endregion
    ...
}
```
You will find the usage of this API in the code of our sample project located at Packages → NexPlayer Simple Sample → NexPlayer → SampleCode → Players → NexPlayerSimple.cs (in Finder: Packages/com.nexplayer.nxplayersimplesample/NexPlayer/SampleCode/Players/NexPlayerSimple.cs) by unfolding the “Widevine” region.

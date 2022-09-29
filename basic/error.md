# Errors

The NexPlayer™ SDK provides a list of virtual functions which begin with “Error”. These allow you to provide custom behavior to answer any NexErrorCode.

## NexPlayerAPI for errors

Error triggered methods inherited from NexPlayerBehaviour:

**protected virtual void ErrorTimeLocked()**
Method triggered by the NexErrorCode PLAYER_ERROR_TIME_LOCKED.
The SDK License is expired.

**protected virtual void ErrorNotActivateAppID()**
Method triggered by the NexErrorCode PLAYER_ERROR_NOT_ACTIVATED_APP_ID.
The current app ID is not activated for the NexPlayer™ SD. If you encounter this error, please contact NexPlayer™ to license your app ID (see the section Technical Support Information).

**protected virtual void ErrorNetwork()**
Method triggered by the NexErrorCode ERROR_NETWORK_PROTOCOL.
Network related error. E.g. socket open fail, connect fail, bind fail, etc.

**protected virtual void ErrorHasNoEffect()**
Method triggered by the NexErrorCode HAS_NO_EFFECT.
The same command has been called already in the same state or the command is invalid. E.g. If an open API is called while processing an open API, the engine does not regard it as an error.

**protected virtual void ErrorInvalidSubtitle()**
Method triggered by the NexErrorCode NEXPLAYER_INVALID_SUBTITLE. 
The subtitles for the video are either invalid or in an unsupported format.

**protected virtual void ErrorInvalidSDK()**
Method triggered by the NexErrorCode PLAYER_ERROR_INVALID_SDK.
NexPlayer™ initialization failed because of an invalid SDK. Error while creating or initializing NexPlayer

**protected virtual void ErrorInit()**
Method triggered by the NexErrorCode PLAYER_ERROR_INIT.
NexPlayer™ initialization failed. Error while creating or initializing NexPlayer.

**protected virtual void ErrorNoLicenseFile()**
Method triggered by the NexErrorCode PLAYER_ERROR_NO_LICENSE_FILE.
NexPlayer™ initialization failed because the License File is missing.

**protected virtual void ErrorSrcNotFound()**
Method triggered by the NexErrorCode NEXPLAYER_ERROR_SRC_NOT_FOUND.
The URI is not supported or not found. Make sure the URI actually exists and check that necessary permissions are set.

**protected virtual void ErrorDRMInit()**
Method triggered by the NexErrorCode DRM_INIT_FAILED.
The content DRM initialization failed. 
E.g. Invalid KeyServer URL (License Acquisition URL).
E.g. Invalid Widevine Headers (keys and/or values).

**protected virtual void ErrorUnknown()**
Method triggered by the NexErrorCode UNKNOWN.
Internal Unknown error. E.g. When memory allocation fails for unknown reasons.

**protected virtual void ErrorURL()**
Method triggered by the NexErrorCode NEXPLAYER_ERROR_URL.
The URL was not found.

**protected virtual void ErrorTimeOut()**
Method triggered by the NexErrorCode SOURCE_OPEN_TIMEOUT.
There is no response from the server within 300 seconds while calling Open().

**protected virtual void ErrorUnhandled(NexErrorCode error)**
The error code received was not handled in Error(NexErrorCode error). This method can be overridden to answer additional error codes

## Sample code for Errors

The following sample code shows how to override inherited virtual methods to respond to any NexPlayer™ error code:

```csharp
public class NexPlayerSimple : NexPlayerBehaviour
{
    protected override void ErrorDRMInit()
    {
        base.ErrorDRMInit();
        // run any custom code
    }
}

```

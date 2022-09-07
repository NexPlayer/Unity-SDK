When you set the property debuglogs to true -> crash on Android

Methods to remove or change from MultistreamController.

##### SetMultiStreamPlayersVisible
This is only using Raw Image -> need to add RenderTexture

##### public bool IsMultiStream()
If using MultistreamController of course we are going to be on multistream.  
Move this method to NexPlayerBehaviour and check whether MultistreamController is initialized and with urls / raw images / render textures.

##### MultiEditHttp()
What is this method doing? Increasing a counter? Wa du heck polisha

##### MultiStreamSetHTTPHeaders()
Wa du heck this method doing again... Adding keys called "Referer" to all player instances. WA DU HECK

##### AllPlayersAreReady()
Change name to **AllPlayersArePlaying**

##### CheckFailedMultiStreams()
THIS IS RETURNING TRUE IF ANY OF THE STREAMS STATE == PAUSE

WA DU HEEEEEECK
# Player integration

The NexPlayer™ Plugin for Unity API allows you to integrate custom video player functionalities through code.

As of version 2.0, NexPlayer™ uses a redesigned architecture, with a clear entry point to the SDK, **NexPlayerBehaviour.cs**. Whereas before it would take several lines of code and extensive reading to control the SDK, now making your own custom player just requires inheriting from **NexPlayerBehaviour.cs**.

The **NexPlayerBehaviour** is designed to simplify the creation of custom players, with no need to add your own boilerplate code. To simplify this many requirements, like loading the plugins and setting up your license, are now handled automatically through the new behaviour. Any custom functionality can be handled by overriding the available virtual functions. By inheriting from **NexPlayerBehaviour** you have access to the main player variables, virtual methods to respond to internal player events, information about internal player errors and other virtual functions to extend the player's default behaviour.

## NexPlayerBehaviour additional functions

You can also control other functionality by overriding virtual functions. When overriding a function remember to always call **base.Function()** and add your custom code below.

**NexPlayerBehaviour** is a Monobehaviour, so you can override all unity events:

- **virtual void Reset()**
- **virtual void Awake()**
- **virtual void OnEnable()**
- **virtual void Start()**
- **virtual void Update()**
- **virtual void OnDisable()**
- **virtual void OnDestroy()**
- **virtual void OnApplicationFocus(bool focus)**
- **virtual void OnApplicationPause(bool pauseStatus)**
- **virtual void OnValidate()**

If needed, make sure to create and destroy the game object that contains the custom player component instead of enabling and disabling it.
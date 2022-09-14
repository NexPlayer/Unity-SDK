# Migrating from previous releases

The namespaces of the following APIs have been changed. Please, make sure to call them correctly.

- Scripts/SampleCode/NexPlayer360/Scripts/NexPlayer360.cs (*)
	NexPlayerAPI -> NexPlayerSample

- Scripts/SampleCode/NexPlayer360/Scripts/NexPlayer360KeyControls.cs (*)
	NexPlayerAPI -> NexPlayerSample

- Scripts/SampleCode/NexPlayer360/Scripts/NexVRInteractable.cs (*)
	NexPlayerAPI -> NexPlayerSample

- Scripts/SampleCode/NexPlayer360/Scripts/NexVRInteractableSeekBar.cs (*)
	NexPlayerAPI -> NexPlayerSample

- Scripts/SampleCode/NexPlayer360/Scripts/NexVRUIController.cs (*)
	NexPlayerAPI -> NexPlayerSample

- Scripts/SampleCode/NexPlayer360/VRMenu/Scripts/MenuAnimator.cs (*)	
	VRStandardAssets.Menu -> NexPlayerSample

- Scripts/SampleCode/NexPlayer360/VRMenu/Scripts/MenuItemPopout.cs (*)
	VRStandardAssets.Menu -> NexPlayerSample

- Scripts/SampleCode/NexPlayer360/VRMenu/Scripts/MenuSelectorMover.cs (*)	
	VRStandardAssets.Menu -> NexPlayerSample

- Scripts/SampleCode/NexPlayer360/VRMenu/Scripts/MenuButton.cs (*)	
	VRStandardAssets.Menu -> NexPlayerSample

- Scripts/SampleCode/NexPlayer360/VRMenu/Scripts/Reticle.cs (*)
	VRStandardAssets.Menu -> NexPlayerSample

- Scripts/SampleCode/NexPlayer360/VRMenu/Scripts/SelectionRadial.cs (*)	
	VRStandardAssets.Menu -> NexPlayerSample

- Scripts/SampleCode/NexPlayer360/VRMenu/Scripts/SelecionSlider.cs (*)
	VRStandardAssets.Menu -> NexPlayerSample

- Scripts/SampleCode/NexPlayer360/VRMenu/Scripts/VRCameraFade.cs (*)
	VRStandardAssets.Menu -> NexPlayerSample

- Scripts/SampleCode/NexPlayer360/VRMenu/Scripts/VREyeRaycaster.cs (*)
	VRStandardAssets.Menu -> NexPlayerSample

- Scripts/SampleCode/NexPlayer360/VRMenu/Scripts/VRCameraUI.cs (*)	
	VRStandardAssets.Menu -> NexPlayerSample

- Scripts/SampleCode/NexPlayer360/VRMenu/Scripts/VRInput.cs (*)	
	VRStandardAssets.Menu -> NexPlayerSample

- Scripts/SampleCode/NexPlayer360/VRMenu/Scripts/VRInteractiveItem.cs (*)
	VRStandardAssets.Menu -> NexPlayerSample

- Scripts/SampleCode/Utility/GameObjectUtil.cs		
	None -> NexUtility
	
- Scripts/SampleCode/Utility/NexHolder.cs	
	NexPlayerSample -> NexUtility

- Scripts/SampleCode/FullFeat/UI/PlaybackSettings.cs		
	NexPlayerAPI -> NexUtility

- Scripts/SampleCode/FullFeat/UI/OfflineStreamingDownload/OfflineStreaming.cs	
	None -> NexUtility		

- Scripts/SampleCode/Editor/NexPlayerEditor.cs (**)	
	NexPlayerAPI ->  NexPlayerSample

- Scripts/SampleCode/Editor/NexPlayerSamplesEditor.cs (**)	
	None->  NexPlayerSample

- Scripts/SampleCode/Editor/NexUIEditor.cs (**)	
	None ->  NexPlayerSample

- Scripts/SampleCode/Editor/NxPMenuItems.cs (**)		
	None ->  NexPlayerSample

- Scripts/SDK/Core/Utility/ID3MetadataHelper.cs
	None ->  NexUtility

- Scripts/Editor/AutoVersion.cs			
	None ->  NexUtility

- Scripts/Editor/ImportManager.cs		
	None -> NexUtility
	
- Scripts/Editor/NexBuildConfigurationHelper.cs
	NexPlayerSample -> NexUtility

- Scripts/Editor/NexBuildConfigurationWindow.cs	
	NexPlayerAPI -> NexUtility

- Scripts/Editor/NexMaterialsEditor.cs		
	None -> NexUtility	

- Scripts/Editor/NexVersionHelper.cs	
	None -> NexUtility
	
- Scripts/Editor/NexVersionHelperEditor.cs	
	NexPlayerSample -> NexUtility

- Scripts/Editor/BuildPostProcessor.cs		
	NexPlayerAPI -> NexPlayerAPI

- Scripts/Editor/PostAndroidManifest.cs	
	None -> NexPlayerAPI	

- Scripts/Editor/PostBuildUtil.cs
	None -> NexPlayerAPI

(*) Moved scripts from NexPlayer/NexPlayer360/ to NexPlayer/Scripts/SampleCode/NexPlayer360/

(**) Moved scripts from NexPlayer/Scripts/Editor/ to NexPlayer/Scripts/SampleCode/Editor/

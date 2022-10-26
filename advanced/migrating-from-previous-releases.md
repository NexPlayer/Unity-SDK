# Migrating from previous releases

The namespaces of the numerous APIs have been changed over time. Please, make sure to address them correctly.

The following scripts were moved from **NexPlayer > NexPlayer360** to **NexPlayer > Scripts > SampleCode > NexPlayer360**:

- **Scripts/SampleCode/NexPlayer360/Scripts/NexPlayer360KeyControls.cs**
	- **Old namespace:** NexPlayerAPI
	- **New namespace:** NexPlayerSample

- **Scripts/SampleCode/NexPlayer360/Scripts/NexVRInteractable.cs**
	- **Old namespace:** NexPlayerAPI
	- **New namespace:** NexPlayerSample

- **Scripts/SampleCode/NexPlayer360/Scripts/NexVRInteractableSeekBar.cs**
	- **Old namespace:** NexPlayerAPI
	- **New namespace:** NexPlayerSample

- **Scripts/SampleCode/NexPlayer360/Scripts/NexVRUIController.cs**
	- **Old namespace:** NexPlayerAPI
	- **New namespace:** NexPlayerSample

- **Scripts/SampleCode/NexPlayer360/VRMenu/Scripts/MenuAnimator.cs**	
	- **Old namespace:** VRStandardAssets.Menu
	- **New namespace:** NexPlayerSample

- **Scripts/SampleCode/NexPlayer360/VRMenu/Scripts/MenuItemPopout.cs**
	- **Old namespace:** VRStandardAssets.Menu
	- **New namespace:** NexPlayerSample

- **Scripts/SampleCode/NexPlayer360/VRMenu/Scripts/MenuSelectorMover.cs**	
	- **Old namespace:** VRStandardAssets.Menu
	- **New namespace:** NexPlayerSample

- **Scripts/SampleCode/NexPlayer360/VRMenu/Scripts/MenuButton.cs**	
	- **Old namespace:** VRStandardAssets.Menu
	- **New namespace:** NexPlayerSample

- **Scripts/SampleCode/NexPlayer360/VRMenu/Scripts/Reticle.cs**
	- **Old namespace:** VRStandardAssets.Menu
	- **New namespace:** NexPlayerSample

- **Scripts/SampleCode/NexPlayer360/VRMenu/Scripts/SelectionRadial.cs**	
	- **Old namespace:** VRStandardAssets.Menu
	- **New namespace:** NexPlayerSample

- **Scripts/SampleCode/NexPlayer360/VRMenu/Scripts/SelecionSlider.cs**
	- **Old namespace:** VRStandardAssets.Menu
	- **New namespace:** NexPlayerSample

- **Scripts/SampleCode/NexPlayer360/VRMenu/Scripts/VRCameraFade.cs**
	- **Old namespace:** VRStandardAssets.Menu
	- **New namespace:** NexPlayerSample

- **Scripts/SampleCode/NexPlayer360/VRMenu/Scripts/VREyeRaycaster.cs**
	- **Old namespace:** VRStandardAssets.Menu
	- **New namespace:** NexPlayerSample

- **Scripts/SampleCode/NexPlayer360/VRMenu/Scripts/VRCameraUI.cs**
	- **Old namespace:** VRStandardAssets.Menu
	- **New namespace:** NexPlayerSample

- **Scripts/SampleCode/NexPlayer360/VRMenu/Scripts/VRInput.cs**	
	- **Old namespace:** VRStandardAssets.Menu
	- **New namespace:** NexPlayerSample

- **Scripts/SampleCode/NexPlayer360/VRMenu/Scripts/VRInteractiveItem.cs**
	- **Old namespace:** VRStandardAssets.Menu
	- **New namespace:** NexPlayerSample

The following scripts were moved from **NexPlayer > Scripts > Editor** to **NexPlayer > Scripts > SampleCode > Editor**:

- **Scripts/SampleCode/Editor/NexPlayerEditor.cs**	
	- **Old namespace:** NexPlayerAPI
	- **New namespace:**  NexPlayerSample

- **Scripts/SampleCode/Editor/NexPlayerSamplesEditor.cs**	
	- **Namespace:**  NexPlayerSample

- **Scripts/SampleCode/Editor/NexUIEditor.cs**	
	- **Namespace:**  NexPlayerSample

- **Scripts/SampleCode/Editor/NxPMenuItems.cs**		
	- **Namespace:**  NexPlayerSample

The following scripts were not moved:

- **Scripts/SampleCode/NexPlayer360/Scripts/NexPlayer360.cs**
	- **Old namespace:** NexPlayerAPI
	- **New namespace:** NexPlayerSample

- **Scripts/SampleCode/Utility/GameObjectUtil.cs**
	- **Namespace:** NexUtility
	
- **Scripts/SampleCode/Utility/NexHolder.cs**	
	- **Old namespace:** NexPlayerSample
	- **New namespace:** NexUtility

- **Scripts/SampleCode/FullFeat/UI/PlaybackSettings.cs**		
	- **Old namespace:** NexPlayerAPI
	- **New namespace:** NexUtility

- **Scripts/SampleCode/FullFeat/UI/OfflineStreamingDownload/OfflineStreaming.cs**
	- **Namespace:** NexUtility		

- **Scripts/SDK/Core/Utility/ID3MetadataHelper.cs**
	- **Namespace:**  NexUtility

- **Scripts/Editor/AutoVersion.cs**			
	- **Namespace:**  NexUtility

- **Scripts/Editor/ImportManager.cs**		
	- **Namespace:** NexUtility
	
- **Scripts/Editor/NexBuildConfigurationHelper.cs**
	- **Old namespace:** NexPlayerSample
	- **New namespace:** NexUtility

- **Scripts/Editor/NexBuildConfigurationWindow.cs**	
	- **Old namespace:** NexPlayerAPI
	- **New namespace:** NexUtility

- **Scripts/Editor/NexMaterialsEditor.cs**
	- **Namespace:** NexUtility	

- **Scripts/Editor/NexVersionHelper.cs**
	- **Namespace:** NexUtility
	
- **Scripts/Editor/NexVersionHelperEditor.cs**	
	- **Old namespace:** NexPlayerSample
	- **New namespace:** NexUtility

- **Scripts/Editor/BuildPostProcessor.cs**		
	- **Old namespace:** NexPlayerAPI
	- **New namespace:** NexPlayerAPI

- **Scripts/Editor/PostAndroidManifest.cs**
	- **Namespace:** NexPlayerAPI	

- **Scripts/Editor/PostBuildUtil.cs**
	- **Namespace:** NexPlayerAPI
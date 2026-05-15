# CSE165 Project 1

A Unity XR project for building and interacting with a virtual medical/lab environment on Meta Quest. The scene includes medical equipment, furniture, a tent/lab setup, locomotion, visual travel indicators, object spawning, single-object manipulation, and group selection/manipulation.

## Project Overview

This project is built around a VR interaction scene where the user can move through the environment, spawn medical objects, select objects with controller rays, and edit objects individually or as groups.

Core features:

- Meta Quest / OpenXR VR support
- Continuous movement and turning with thumbsticks
- Travel direction indicators for movement and turning
- Spawn menu for placing single or multiple prefabs
- Ray-based single-object selection
- Move, rotate, and scale manipulation modes
- Group selection, group manipulation, and duplication
- Runtime setup for selectable medical objects

## Requirements

- Unity `6000.4.1f1`
- Meta Quest headset or compatible OpenXR setup
- Android Build Support installed in Unity Hub
- USB debugging enabled on the Quest for device builds

Important packages are managed through `Packages/manifest.json`, including:

- Meta XR SDK All `201.0.0`
- XR Interaction Toolkit `3.4.1`
- XR Management `4.6.0`
- OpenXR `1.16.1`
- Meta OpenXR `2.5.0`
- Unity Input System `1.19.0`
- TextMesh Pro / UGUI

## Opening the Project

1. Open Unity Hub.
2. Add this project folder.
3. Open it with Unity `6000.4.1f1`.
4. Wait for Unity to restore packages and import assets.
5. Open `Assets/Scenes/SampleScene.unity`.

The main scene is configured for a Meta Quest Android build profile and uses the XR/OpenXR project settings already included in the repository.

## Controls

### Idle Controls

- Left Trigger: open the spawn menu
- Left Grip: open group selection
- Right Grip: open single-object ray selection
- Left Thumbstick: move
- Right Thumbstick: turn

### Spawn Menu

- Right Trigger: cycle through spawnable prefabs
- Right Grip: toggle a prefab for multi-spawn
- Left Grip: start placement
- Left Trigger: cancel or exit

During placement:

- The preview follows the controller ray.
- Right Trigger enters rotation mode.
- Left Trigger cancels placement.

During rotation:

- Hold Right Trigger: rotate the preview
- Right Grip: confirm spawn
- Left Trigger: return to placement

### Single Selection

- Right Grip: enter ray selection mode
- Right Trigger: select the hovered object
- Left Trigger: exit selection/manipulation

After selecting an object:

- Hold Right Trigger: manipulate the object
- Right Grip: switch mode between Move, Rotate, and Scale
- Left Trigger: back/exit

### Group Selection

- Left Grip: open group selection menu
- Left/Right Trigger: move cursor
- Right Grip: toggle selected object
- Left Grip: start group edit

During group manipulation:

- Right Trigger: use the current manipulation mode
- Left Trigger: switch mode between Move, Rotate, and Scale
- Right Grip: duplicate selected group
- Left Grip: exit group manipulation

## Key Files

- `Assets/Scenes/SampleScene.unity` - main VR scene
- `Assets/Scripts/TravelRigController.cs` - thumbstick movement and turning
- `Assets/Scripts/TravelIndicator.cs` - movement and turn visual indicators
- `Assets/Scripts/SpawnMenu.cs` - VR spawn menu and placement workflow
- `Assets/Scripts/SelectionManipulator.cs` - single-object ray selection/manipulation
- `Assets/Scripts/GroupSelectionManipulationVR.cs` - group selection, editing, and duplication
- `Assets/Scripts/RuntimeInteractableSetup.cs` - runtime setup for selectable objects
- `Assets/Scripts/SelectableObject.cs` - highlight state for selected objects
- `Assets/Assets/Spawnable Prefabs/` - prefabs available to the spawn menu
- `Assets/Assets/Medical equipment/` - imported medical environment assets
- `Assets/Assets/Tent/` - tent environment asset
- `Assets/Assets/VrLab/` - lab furniture assets

## Building for Meta Quest

1. Connect the Quest headset with USB debugging enabled.
2. In Unity, open `File > Build Profiles`.
3. Select the `Meta Quest` build profile.
4. Confirm the target platform is Android.
5. Build and run to deploy to the headset.

Project settings currently use:

- Product name: `My project`
- Version: `0.1`
- Android minimum SDK: `32`
- Android target SDK: `34`
- ARM64 Android target architecture
- OpenXR/Meta Quest support

## Notes for Development

- The root scene automatically configures objects whose names start with `Medical_`, `Equipment_`, or `Package_` as selectable objects.
- Spawned objects are also configured at runtime so they can be selected and manipulated.
- The selectable object layer is currently hard-coded as layer `3` in `RuntimeInteractableSetup.cs`.
- The UI menu canvas is shared across spawn, single selection, and group selection systems.
- Generated Unity files such as `.csproj` and `.slnx` files may change when Unity regenerates the project.

## Repository Layout

```text
Assets/
  Assets/
    Medical equipment/
    Spawnable Prefabs/
    Tent/
    VrLab/
  Scenes/
  Scripts/
  XR/
Packages/
ProjectSettings/
```

## Troubleshooting

- If controller input does not work, check that the Quest controllers are active and that OpenXR/Meta Quest support is enabled in Project Settings.
- If objects cannot be selected, confirm they have colliders and are on the selectable layer.
- If spawned objects are not interactable, check that `RuntimeInteractableSetup.ConfigureInteractableHierarchy` is being called after spawning.
- If the build target is wrong, switch to the included `Meta Quest` build profile before building.

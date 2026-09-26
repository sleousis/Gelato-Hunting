# Gelato Hunting

Gelato Hunting is a small 2D mobile arcade game made in Unity. Ice cream scoops fall from the top of the screen and you move a cup left and right to catch them. Missed scoops cost a life. Special scoops double the score, grow or shrink the cup, or slow time. Earned coins buy new cups and backgrounds in an in-game store. The project was built for Android and iOS under the team name "Guacamole".

This repository holds the Unity project (assets, scenes, scripts and settings). It does not contain a built game.

> **Not run in Unity.** During the 2026 maintenance pass the Unity Editor was not installed. The project was not opened, compiled or played. The scripts were only checked by reading them.

## Contents

- Three scenes: a splash screen, the main menu (with an AI player catching scoops in the background, high scores, store and settings) and the game scene.
- C# gameplay scripts for the player cup, falling scoops, power ups, lives, score, levels, pause and the store.
- 2D textures, animations, prefabs, fonts and sounds.
- Two small third-party asset packs: "Simple Scene Fader" and "Small particle pack".

## Tech stack

- Unity **2018.2.9f1** (from `ProjectSettings/ProjectVersion.txt`)
- C# scripts only. `Assets/Small particle pack/TimedObjectDestructor.cs` was ported from UnityScript (`.js`) in 2026 with the same GUID and fields, so the confetti prefab still points at it
- Unity packages pinned in `Packages/manifest.json` (TextMesh Pro 1.2.4, Ads 2.0.8, Analytics 2.0.16, Purchasing 2.0.3 and the built-in modules)
- Target platforms in the project settings: Android (min SDK 16) and iOS

## Repository layout

```
Assets/
  _Scenes/              splash.unity, menu.unity, scene.unity
  Scripts/              game scripts (GameManager, PlayerController, Absorber, AI, StoreSelect, ...)
  Prefabs/              scoops, cups and menu AI prefabs
  2D Textures/          backgrounds, cups, flavors, UI, logos, store icons
  Animations/           UI and effect animations
  Fonts/                LuckiestGuy and Primer
  Sounds/               music and sound effects
  Simple Scene Fader/   third-party scene fade helper
  Small particle pack/  third-party confetti particles
  ProjectSettings/      an old copy of project settings from Unity 5.4 (not used by the editor)
Packages/manifest.json  Unity package list
ProjectSettings/        the real project settings
```

## Prerequisites

- Unity Hub
- Unity Editor **2018.2.9f1** (install it from the Unity download archive)
- Android Build Support and/or iOS Build Support modules if you want to build for phones

## Setup

1. Clone the repository.
2. In Unity Hub choose "Add" (or "Open") and pick the repository folder.
3. Open it with Unity 2018.2.9f1. Unity rebuilds the `Library/` folder and the `.csproj` and `.sln` files on first open. These are generated files and are ignored by git.

## How to run (not verified)

These steps are the standard Unity workflow. They were not tried in this maintenance pass.

1. Open `Assets/_Scenes/splash.unity`.
2. Press Play in the editor. The splash screen moves on to the menu, and "Play" loads the game scene.
3. To build, open File > Build Settings. The three scenes are already listed in order (splash, menu, scene). Pick Android or iOS and build.

Controls: hold the left mouse button (or touch the screen) in the lower part of the screen to move the cup. A right click saves a screenshot (a leftover debug feature).

## Notes and known limitations

- **Not tested.** No Unity Editor was available. Nothing was compiled or run. Reading the C# scripts found no obvious compile errors for Unity 2018.2.
- **Unity version.** The project was last saved with 2018.2.9f1. An upgrade to Unity 6 (6000.6.3f1, the latest stable release on 2026-09-26) is planned but not done yet. The Unity Editor could not be installed in this pass. Newer versions may need package upgrades in `Packages/manifest.json`.
- **Old settings copy.** `Assets/ProjectSettings/` is a leftover copy of settings from Unity 5.4.0f3. Unity ignores it. It was kept as it was.
- **Scene paths.** The build settings list scenes as `assets/_Scenes/...` in lower case. This works on Windows. A case-sensitive file system may need them fixed in Build Settings.
- **Signing.** The Android keystore is not in the repository. The settings point to a keystore path on another machine, so you need your own keystore to make a release build.
- **Google Play Games.** The Play Games code is commented out. `GelatoHuntingResources.cs` still holds the leaderboard and achievement ids.
- Save data (coins, high scores, purchases, settings) is kept in Unity `PlayerPrefs`.

## Authors

Savvas Leousis (sleousis), as part of the team "Guacamole".

# Gelato Hunting

Gelato Hunting is a small 2D mobile arcade game made in Unity. Ice cream scoops fall from the top of the screen and you move a cup left and right to catch them. Missed scoops cost a life. Special scoops double the score, grow or shrink the cup, or slow time. Earned coins buy new cups and backgrounds in an in-game store. The project was built for Android and iOS under the team name "Guacamole".

This repository holds the Unity project (assets, scenes, scripts and settings). A ready-to-play Windows build is on the Releases page.

The project was first made with Unity 5.4 and last saved with Unity 2018.2.9f1. In September 2026 it was upgraded to Unity 6 (**6000.6.3f1**, the latest stable release at the time). It compiles with no errors, and the Windows build was played after the upgrade.

## Download

Get `GelatoHunting-v1.0.0-windows-x64.zip` from the [Releases page](https://github.com/sleousis/Gelato-Hunting/releases). Extract it anywhere and run `Gelato Hunting.exe`. It needs 64-bit Windows 10 or 11. Hold the left mouse button in the lower part of the window and move the mouse to steer the cup. To play in a phone-shaped window, start it from a command prompt with `"Gelato Hunting.exe" -screen-fullscreen 0 -screen-width 540 -screen-height 960`.

## Contents

- Three scenes: a splash screen, the main menu (with an AI player catching scoops in the background, high scores, store and settings) and the game scene.
- C# gameplay scripts for the player cup, falling scoops, power ups, lives, score, levels, pause and the store.
- 2D textures, animations, prefabs, fonts and sounds.
- Two small third-party asset packs: "Simple Scene Fader" and "Small particle pack".

## Tech stack

- Unity **6000.6.3f1** (changeset 45d8eee7de74), set in `ProjectSettings/ProjectVersion.txt`. Before 2026 it was 2018.2.9f1.
- C# scripts only. `Assets/Small particle pack/TimedObjectDestructor.cs` was ported from UnityScript (`.js`) in 2026 with the same GUID and fields, so the confetti prefab still points at it. Unity 6 no longer compiles UnityScript.
- Unity packages pinned in `Packages/manifest.json` and `Packages/packages-lock.json`. The upgrade moved them to the versions Unity 6000.6.3f1 picks: Ads 4.19.0, Analytics 3.8.2, Purchasing 4.15.0, uGUI 2.6.0 (which now contains TextMesh Pro) and the built-in modules.
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
Packages/               manifest.json and packages-lock.json (Unity package list)
ProjectSettings/        the real project settings
```

## Prerequisites

- Unity Hub (3.21.3 was used)
- Unity Editor **6000.6.3f1**. Windows standalone (Mono) support is included with the Windows editor.
- A Unity license. A free Personal license works. Sign in to Unity Hub and activate it before using batch mode.
- Android Build Support or iOS Build Support modules only if you want to build for phones

## Setup

1. Clone the repository.
2. In Unity Hub choose "Add" (or "Open") and pick the repository folder.
3. Open it with Unity 6000.6.3f1. Unity rebuilds the `Library/` folder and the `.csproj` and `.slnx` files on first open. These are generated files and are ignored by git.

## Build from the command line

These commands were run on Windows 11 (Git Bash) in September 2026. The editor was installed at `D:\Apps\Unity\6000.6.3f1`. Change the paths for your machine.

Open (import and compile) the project in batch mode:

```
"D:/Apps/Unity/6000.6.3f1/Editor/Unity.exe" -batchmode -nographics -accept-apiupdate \
  -projectPath "D:\Git\Gelato-Hunting" -logFile "D:\Git\Gelato-Hunting\Logs\upgrade.log" -quit
```

Result: exit code 0, no `error CS` lines in the log, and "Exiting batchmode successfully now!".

Build a Windows 64-bit player into `Builds/Windows` (ignored by git):

```
"D:/Apps/Unity/6000.6.3f1/Editor/Unity.exe" -batchmode -nographics -projectPath "D:\Git\Gelato-Hunting" \
  -buildTarget Win64 -buildWindows64Player "D:\Git\Gelato-Hunting\Builds\Windows\Gelato Hunting.exe" \
  -logFile "D:\Git\Gelato-Hunting\Logs\build.log" -quit
```

Result: exit code 0 and "Build Finished, Result: Success." in the log.

The built player was started once for 15 seconds with `"Builds/Windows/Gelato Hunting.exe" -batchmode -nographics -logFile Logs/player.log`. The log shows two scene loads (splash, then menu) and no exceptions or errors.

On Linux or macOS the flags are the same. Use the path of the Unity binary on that system and `-buildTarget Linux64 -buildLinux64Player <path>` (not tried).

## How to play in the editor (not verified)

1. Open `Assets/_Scenes/splash.unity`.
2. Press Play. The splash screen moves on to the menu, and "Play" loads the game scene.
3. To build for phones, open File > Build Profiles. The three scenes are listed in order (splash, menu, scene). Pick Android or iOS and build.

Controls: hold the left mouse button (or touch the screen) in the lower part of the screen to move the cup. A right click saves a screenshot (a leftover debug feature).

## Notes and known limitations

- **Testing.** The Windows build was played on Windows 11. The menu, Instructions, Store, High Scores and About screens open. Rounds start, scoops fall, missed scoops cost lives, Game Over and Retry work, and scores are saved to the high score table. The player log had no errors. The Android and iOS builds were not tried.
- **Compiler warnings.** Unity 6 warns that `Object.FindObjectsOfType` (in `AI_PlayerController.cs`) and `Rigidbody2D.velocity` (in `RandomLerp.cs`) are obsolete. They still work, so the code was left as it was.
- **Upgrade side effects.** Unity rewrote the texture `.meta` files, `ProjectSettings/` and `Packages/manifest.json` for the new version. It removed `UnityAdsSettings.asset`. The Ads, Analytics and Purchasing packages jumped several major versions. The game code does not call them, but the Unity services they need were not set up or tested.
- **Old settings copy.** `Assets/ProjectSettings/` is a leftover copy of settings from Unity 5.4.0f3. Unity ignores it. It was kept as it was.
- **Scene paths.** The build settings list scenes as `assets/_Scenes/...` in lower case. This works on Windows. A case-sensitive file system may need them fixed in Build Settings.
- **Signing.** The Android keystore is not in the repository. The settings point to a keystore path on another machine, so you need your own keystore to make a release build.
- **Google Play Games.** The Play Games code is commented out. `GelatoHuntingResources.cs` still holds the leaderboard and achievement ids.
- Save data (coins, high scores, purchases, settings) is kept in Unity `PlayerPrefs`.

## Authors

Savvas Leousis (sleousis), as part of the team "Guacamole".

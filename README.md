# All Star Tower Defense

**Being maintained by JEIKARU (again).** The source code has been released as `astd.lua`. If you use the source code, please credit **KarmaPanda**.

The original release was reported as tested and working. The latest changes documented below have not been tested inside Roblox.

The latest source provided with this README is [astd.lua](https://raw.githubusercontent.com/Jeikaru/Roblox-1/refs/heads/main/astd.lua).

## Script Features

### Main

```text
Auto Unit Buff
Auto Extreme
Auto 2x Speed
Auto 3x Speed
Auto Replay
Auto Next Story / Next Room
Mini GUI
Facility Floating Toggle Button
K Key to Show / Hide the Interface
Single UI per Session — Duplicate Execution Guard
```

### Macro

```text
Profile Select
Record Macro
Playback Macro
Previous Macro Step
Next Macro Step
Reset Macro Step
New Name Macro Profile
Create Macro Profile
Delete Selected Macro Profile
Clear Selected Macro Profile Data
Recording Options
Time Recording Offset
Playback Options
Money Tracking
Playback Time Offset
Magnitude
Attempt Before Action Skip
Action Skip Search Delay
Macro Options
Elapsed Time Mode (V1, V2)
Summon Unit
Sell Unit
Upgrade Unit
Unit Ability
Auto Unit Ability
Skip Wave
Auto Skip Wave
Ability Blacklist Configuration
Searchable Blacklisted Unit List
Searchable Unit List
Add Selected Unit from Unit List to Ability Blacklist
Delete Selected Blacklisted Unit from Ability Blacklist
```

### Lobby

```text
Auto Join Game
Auto Join Tower
Auto Evolve EXP Unit
Auto Click Popup
Auto Join Settings
Delay
Mode
Story Level
Automatic Story Level Detection and Saving
Infinite Map Selection
Automatic Adventure Map Detection
Searchable Adventure Map Selection
Adventure Map List Refreshes Every Two Seconds
```

### Webhooks

```text
Webhook Settings
Webhook URL
Discord ID
Ping User
Test Webhook
Webhook Color
Toggles
Send Webhook on Game End
Send Webhook after EXP Evolve
```

### Advanced Settings

```text
Auto Unit Buffing Settings
Searchable Configured Units
Searchable Unit List
Buffing Mode (Box, Pair, Cycle, Spam)
Attack Buff Check
Range Buff Check
Multiple Abilities Check
Multiple Abilities Name
Ability Time
Cycle Units
Post Loop Delay
Edit Auto Unit Buffing Settings
Save Auto Unit Buffing Settings
Add Selected Unit from Unit List to Auto Buff
Delete Selected Auto Buff Unit from Auto Buff
Action Queue Settings
Remote Action Delay
Remote Refiring
Refire Remote
Pre Loop Delay
Loop Delay
Automation Settings
Auto Battle Gems
Auto Upgrade Money
Auto Upgrade Wave
Stop Auto Upgrade at Wave
Auto Sell at Wave
```

### Miscellaneous

```text
Game Settings
FPS Boost
Anti-AFK
Disable 3D Rendering
Anonymous Mode
Change Anonymous Name
World Teleports
Teleport to World 1
Teleport to World 2
Reset Settings to Default
Auto Execute
```

### Credits

```text
Original Author: KarmaPanda
Maintainer: JEIKARU
Facility UI Credits
Community Discord Link
```

Available controls can depend on the current world or whether you are in the lobby. Expect bugs on Auto Join, Macro is fully working except on other executors. Delta Mobile and Real Works.

## Discord Server

[Join the Discord server](https://discord.gg/BrnQQGKbvE)

## Facility UI Update

## Rayfield → Facility migration

Converted the interface to Facility while retaining the existing gameplay logic and settings system.

### Changed

- Replaced the Rayfield loader with the Facility loader.
- Converted all **7 tabs and 102 controls** to Facility:
  - Main
  - Macro
  - Lobby
  - Webhooks
  - Advanced Settings
  - Miscellaneous
  - Credits
- Organized controls into Facility full-width sections with side navigation.
- Set the main window to 760 × 640 and updated its title and UI credits.
- Converted toggles, buttons, inputs, sliders, dropdowns, paragraphs, and the webhook color picker.
- Converted notifications to Facility's notification format.
- Updated dropdown defaults, selection reads, selection changes, and option-list refreshes to Facility's API.
- Preserved multiple selection for Auto Buff Checks.
- Mapped slider ranges and increments to Facility's minimum, maximum, step, and decimal settings.
- Restored saved toggle states silently during UI construction to avoid starting duplicate automation loops.
- Replaced the external hide-button loader with Facility's floating toggle button.

### Preserved

- Existing gameplay and automation functions.
- Macro recording, playback, profile management, and import logic.
- Existing settings and macro storage paths and formats.
- Existing webhook logic and settings.
- The custom playback mini GUI.
- **K** as the main interface toggle key.
- Original author and maintainer credits, plus the Discord link in Credits.

### Differences from the Rayfield version

- Rayfield's automatic Discord invite prompt is no longer included.
- Rayfield's loading screen and built-in control search were not recreated.
- The script continues to use its own settings persistence; Facility's SaveManager and theme settings screens were not added.
- The webhook color picker remains color-only, with opacity editing disabled.

### Validation

- Confirmed that all 7 tabs and 102 controls were converted.
- Checked section and notification counts against the original source.
- Checked balanced delimiters, dropdown value shapes, and decimal slider settings.
- Confirmed that the gameplay body remained unchanged except for notification calls and the hide-button integration.
- Confirmed that the Rayfield loader and old control creation calls were removed.

**Testing limitation:** These were static checks, not a Luau compilation or a Roblox runtime test. In-game behavior still needs verification.

### Files and usage

- Press **K** or use the floating toggle button to show or hide the main interface.
- The script loads Facility from its configured GitHub `main` branch at runtime, so it requires access to that source and may receive upstream library changes.

**The script version is 4.0; this update changes the UI integration without assigning a new release version.**

## Additional script updates

## Automatic Adventure map detection

- Replaced the hardcoded Adventure map list with numeric children from `PlayerGui.HUD.MissionsV2.MissionChooser.Main.Challenges`.
- Reads each card's `MissionTitle.Text` for its map name and keeps its ID as a string.
- Refreshes the Adventure dropdown every two seconds as entries or titles change.
- Reads already-loaded cards without opening the mission chooser.
- Sorts map choices alphabetically and adds IDs to distinguish duplicate names.
- Preserves the saved map selection while the game's map list is unavailable.

## Searchable unit lists

- Enabled search inside the auto-buff Unit List and configured Units dropdowns.
- Enabled search inside the blacklist Unit List and Blacklisted Units dropdowns.
- Enabled search in the Adventure map dropdown.
- Added checks to prevent adding invalid placeholder selections as units.

Open a dropdown and type in its search field to filter the choices.

## Automatic Story Level detection

- Reads saved story progress using `Server:InvokeServer("Data", "StoryLevel")`.
- Saves the returned numeric level directly to the existing Story Level setting.
- Runs on startup and before Story auto-join.
- Updates the Story Level control when it is available.
- Keeps the previous setting if the request fails or returns an invalid level.

The detector does not require the game's story UI to be open. It applies no level offset. EX Story automation and automatic `+5` progression were not added.

## Single Facility UI per session

- Added a shared session guard before initialization.
- Repeated execution shows the existing Facility UI and stops the duplicate execution.
- Prevents repeated execution from creating additional windows or starting another copy of the script's automation loops.
- Blocks overlapping initialization while the first execution is still loading.
- Reports startup failures; a partial session that already created the library requires a rejoin before retrying.

Rejoin before switching from an older version to this one. The guard does not remove copies started by older versions.

## Edit Auto Unit Buffing Settings

Added **Edit Auto Unit Buffing Settings** and **Save Auto Unit Buffing Settings** buttons for existing configured units.

Editable fields:

- Buffing mode: Box, Pair, Cycle, or Spam.
- Auto Buff Checks: Attack Buff, Range Buff, and Multiple Abilities.
- Ability name for Multiple Abilities.
- Ability time.
- Cycle units.
- Post-loop delay, including tenths of a second such as `0.5`.

### How to edit

1. Open **Advanced Settings → Auto Unit Buffing Settings**.
2. Select an existing configured unit under **Units**.
3. Click **Edit Auto Unit Buffing Settings** to load its saved values.
4. Change the fields above the edit buttons.
5. Click **Save Auto Unit Buffing Settings**.

Saving updates the selected unit's information and persists the settings. Existing buff loops read the changes on a subsequent loop; an action already underway may finish with its earlier values. Newly added units require a rejoin and script execution.

### Validation

- Ability time must be a finite number greater than zero.
- Multiple Abilities requires a nonempty ability name.
- Changing the selected unit requires clicking Edit again before saving to it.
- Saving edits to a removed unit is blocked.
- Add and edit actions use the same field validation.

## Verification status

Changes were reviewed by Jeikaru and yet. Expect bugs on new things.

Auto Ai Place soon. i need to fix the ai placement function first so that it doesnt have any errors on putting units in paths while changing the value.

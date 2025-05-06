# T1Router - Route Plugin for Tribes 1

It's a plugin for Tribes 1 (1.40) that allows players to record their routes and then display them as visual markers in-game.

## Features

*   **Route Recording:** Record your player's position and velocity at set intervals.
*   **Route Saving:**
    *   Routes are saved automatically as `MapName_Team_Route#.txt`.
    *   Saved to a `MyRoutes` subfolder within your user's "My Documents" directory (created automatically if it doesn't exist).
    *   Users can rename the `.txt` files to be more descriptive (e.g., "BE west fast.txt").
*   **Route Playback:**
    *   Load saved routes from the in-game menu.
    *   Displays the route as a series of connected visual markers in the game world.
    *   Start, end, and intermediate points are color-coded for clarity.
    *   **Occlusion Culling:** Markers behind terrain or geometry are hidden (needs refinement).
    *   **Progress Tracking:** Passed markers are automatically hidden as you move along the route.
    *   **Catch-up Mechanic:** If you deviate significantly but rejoin the route further along, the playback will attempt to catch up to your current position on the path (needs refinement).
*   **In-Game UI:**
    *   Access a menu to manage recording and playback.
    *   List available routes for the current map found in your `MyRoutes` folder.
    *   Refresh the route list.
    *   Unload the currently displayed route.
*   **Customizable Keybinds:**
    *   Change the keys for toggling the menu, starting recording, and stopping/saving recording via the in-game UI.
    *   Keybinds are saved to `T1RouterSettings.ini` in the plugins folder in your Tribes directory.

## Installation

1.  **Download:** Obtain the latest `T1Router.dll` file from the [Releases page](https://github.com/shadoh420/T1Router_public/releases).
2.  **Locate Game Directory:** Find your Starsiege: Tribes installation directory.
3.  **Move DLL:**
    *   Place `T1Router.dll` into the `plugins` folder.

## How to Use

1.  **Launch Tribes.** 
2.  **Toggle Menu:**
    *   Default Key: `INSERT`
    *   Press this key to open/close the "Route Tool" menu.
    *   You can rebind this key in the menu.
3.  **Recording a Route:**
    *   Navigate to the map and join the team you wish to record for.
    *   Press the **Start Recording** key (Default: `HOME`). You should see the status in the menu change to "RECORDING" (close the menu to free the cursor).
    *   Run your route. The plugin will save your position and velocity at regular intervals (currently every 250ms).
    *   Press the **Stop/Save Record** key (Default: `END`). The recording will stop, and the route will be saved to `My Documents\MyRoutes\MapName_Team_Route#.txt`. The `#` will be an incrementing number.
    *   You can then go to your `Documents\MyRoutes` folder and rename the `.txt` file to something more descriptive if you wish. The internal map name is used for filtering.
4.  **Playing Back a Route:**
    *   Ensure you are on the map for which you want to load a route.
    *   Open the "Route Tool" menu (`INSERT` or your custom key).
    *   Click the **"Refresh Route List (Current Map)"** button. This will scan your `MyRoutes` folder for compatible route files for the map you are currently on.
    *   Select a route from the "Available Routes" list by clicking its name.
    *   The route markers should now appear in-game.
    *   Close the menu (`INSERT` or your custom key) to get a better view.
    *   As you move along the path and get close to markers, they will disappear, and the "Next Target Index" in the menu will update.
    *   To stop displaying the current route, open the menu and click **"Unload Route"**.
5.  **Customizing Keybinds:**
    *   Open the "Route Tool" menu.
    *   Scroll down to the "Keybinds" section.
    *   Click the button next to the action you want to change (e.g., next to "Toggle Menu: INSERT").
    *   The button text will change to `<Press any key>`.
    *   Press the new keyboard key you want to assign to that action.
    *   Press `ESC` to cancel key capture.
    *   Keybinds are saved automatically to `T1RouterSettings.ini`.

## Configuration File (`T1RouterSettings.ini`)

This file is automatically created in the `plugins` directory (inside your Tribes folder) when you first change a keybind or when the plugin first attempts to load settings. It stores your custom keybinds.

Example:
```ini
[Settings]
StartRecordKey=36    ; VK_HOME
StopRecordKey=35     ; VK_END
ToggleMenuKey=45     ; VK_INSERT
```

Libraries used:

Dear ImGui: For the UI framework.

Microsoft Detours: For function hooking.

GLM: For mathematics.

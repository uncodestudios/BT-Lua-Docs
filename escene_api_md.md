# Scene API

Scene management and application control functions for Lua mods.

## Scene Loading

**LoadScene(sceneName)** - Load scene by name
```lua
EScene:LoadScene("MainMenu")
```

**LoadSceneAsync(sceneName)** - Load scene asynchronously
```lua
EScene:LoadSceneAsync("Level2") -- Non-blocking load
```

**LoadSceneByIndex(sceneIndex)** - Load scene by build index
```lua
EScene:LoadSceneByIndex(1) -- Load second scene in build settings
```

**LoadSceneAdditive(sceneName)** - Load scene additively (keep current scene)
```lua
EScene:LoadSceneAdditive("UI_Overlay") -- Add to current scene
```

**UnloadScene(sceneName)** - Unload additive scene
```lua
EScene:UnloadScene("UI_Overlay")
```

## Scene Information

**GetActiveSceneName()** - Get current scene name
```lua
local currentScene = EScene:GetActiveSceneName()
Debug:Log("Current scene: " .. currentScene)
```

**GetActiveSceneIndex()** - Get current scene build index
```lua
local sceneIndex = EScene:GetActiveSceneIndex()
```

**GetSceneCount()** - Get number of loaded scenes
```lua
local loadedScenes = EScene:GetSceneCount()
```

**GetSceneCountInBuildSettings()** - Get total scenes in build
```lua
local totalScenes = EScene:GetSceneCountInBuildSettings()
```

## Scene Navigation

**ReloadScene()** - Reload current scene
```lua
EScene:ReloadScene()
```

**LoadNextScene()** - Load next scene in build order
```lua
EScene:LoadNextScene() -- Cycles back to first if at end
```

**LoadPreviousScene()** - Load previous scene in build order
```lua
EScene:LoadPreviousScene() -- Cycles to last if at beginning
```

## Time Control

**SetTimeScale(timeScale)** - Set game time scale
```lua
EScene:SetTimeScale(0.5) -- Half speed
EScene:SetTimeScale(2.0) -- Double speed
EScene:SetTimeScale(0.0) -- Pause
```

**GetTimeScale()** - Get current time scale
```lua
local timeScale = EScene:GetTimeScale()
```

**PauseGame()** - Pause the game (sets time scale to 0)
```lua
EScene:PauseGame()
```

**ResumeGame()** - Resume the game (sets time scale to 1)
```lua
EScene:ResumeGame()
```

**IsGamePaused()** - Check if game is paused
```lua
if EScene:IsGamePaused() then
    Debug:Log("Game is paused")
end
```

## Application Control

**QuitGame()** - Quit the application
```lua
EScene:QuitGame()
```

**OpenURL(url)** - Open URL in browser
```lua
EScene:OpenURL("https://example.com")
```

## Performance Settings

**SetTargetFrameRate(frameRate)** - Set target FPS (-1 for unlimited)
```lua
EScene:SetTargetFrameRate(60) -- Cap at 60 FPS
EScene:SetTargetFrameRate(-1) -- Unlimited FPS
```

**GetTargetFrameRate()** - Get target FPS
```lua
local targetFPS = EScene:GetTargetFrameRate()
```

**SetVSyncCount(vSyncCount)** - Set VSync (0=off, 1=on, 2=every second frame)
```lua
EScene:SetVSyncCount(1) -- Enable VSync
EScene:SetVSyncCount(0) -- Disable VSync
```

**GetVSyncCount()** - Get VSync setting
```lua
local vsync = EScene:GetVSyncCount()
```

## Application Info

**GetApplicationVersion()** - Get app version
```lua
local version = EScene:GetApplicationVersion()
Debug:Log("Game version: " .. version)
```

**GetPlatform()** - Get current platform
```lua
local platform = EScene:GetPlatform()
Debug:Log("Platform: " .. platform) -- "WindowsPlayer", "OSXPlayer", etc.
```

**IsFocused()** - Check if application has focus
```lua
if EScene:IsFocused() then
    Debug:Log("Game window is focused")
end
```

**IsPlaying()** - Check if game is playing (not in editor)
```lua
if EScene:IsPlaying() then
    Debug:Log("Game is running")
end
```

## Background Behavior

**SetRunInBackground(runInBackground)** - Set if game runs when unfocused
```lua
EScene:SetRunInBackground(true) -- Keep running when unfocused
```

**GetRunInBackground()** - Check background running setting
```lua
local runsInBackground = EScene:GetRunInBackground()
```

## File Paths

**GetDataPath()** - Get game data folder path
```lua
local dataPath = EScene:GetDataPath()
Debug:Log("Data path: " .. dataPath)
```

**GetPersistentDataPath()** - Get persistent data folder path
```lua
local savePath = EScene:GetPersistentDataPath()
Debug:Log("Save path: " .. savePath)
```

**GetStreamingAssetsPath()** - Get streaming assets folder path
```lua
local streamingPath = EScene:GetStreamingAssetsPath()
```

**GetTemporaryCachePath()** - Get temporary cache folder path
```lua
local tempPath = EScene:GetTemporaryCachePath()
```

## Object Persistence

**DontDestroyOnLoad(obj)** - Keep object when loading scenes
```lua
local musicManager = Engine:FindGameObject("MusicManager")
EScene:DontDestroyOnLoad(musicManager) -- Survives scene changes
```

## Example
```lua
function Start()
    Debug:Log("Current scene: " .. EScene:GetActiveSceneName())
    Debug:Log("Platform: " .. EScene:GetPlatform())
    
    -- Set performance settings
    EScene:SetTargetFrameRate(60)
    EScene:SetVSyncCount(1)
    
    -- Keep music playing between scenes
    local music = Engine:FindGameObject("BackgroundMusic")
    if music then
        EScene:DontDestroyOnLoad(music)
    end
end

function Update()
    -- Pause with P key
    if EInput:GetKeyDown("p") then
        if EScene:IsGamePaused() then
            EScene:ResumeGame()
            Debug:Log("Game resumed")
        else
            EScene:PauseGame()
            Debug:Log("Game paused")
        end
    end
    
    -- Scene navigation
    if EInput:GetKeyDown("n") then
        EScene:LoadNextScene()
    end
    
    if EInput:GetKeyDown("r") then
        EScene:ReloadScene()
    end
    
    -- Slow motion with left shift
    if EInput:IsShiftHeld() then
        EScene:SetTimeScale(0.3)
    else
        EScene:SetTimeScale(1.0)
    end
    
    -- Quit with Escape
    if EInput:IsEscapePressed() then
        EScene:QuitGame()
    end
end
```

## Notes
- Scene names must match exactly (case-sensitive)
- Scene indices start from 0
- Time scale affects physics, animations, and coroutines
- DontDestroyOnLoad objects persist until manually destroyed
- VSync and target framerate work together to control performance
- Persistent data path is writable and survives game updates
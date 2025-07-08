# External Object API

Load external assets (3D models and audio) at runtime for Lua mods.

## 3D Model Loading

**LoadGLB(relativePath, callbackFunctionName, modName)** - Load GLB/GLTF model asynchronously
```lua
EObject:LoadGLB("EAssets/Models/MyModel.glb", "onModelLoaded", "MyMod")
```

### Model Loading Callback
```lua
function onModelLoaded(gameObject)
    if gameObject then
        Debug:Log("Model loaded: " .. gameObject.name)
        Engine:SetPosition(gameObject, 0, 0, 5)
        Engine:SetScale(gameObject, 2, 2, 2)
    else
        Debug:LogError("Failed to load model")
    end
end
```

## Audio Loading

**LoadAudio(relativePath, callbackFunctionName, modName)** - Load audio file asynchronously
```lua
EObject:LoadAudio("EAssets/Audio/mySound.ogg", "onAudioLoaded", "MyMod")
```

### Audio Loading Callback
```lua
function onAudioLoaded(audioClip)
    if audioClip then
        Debug:Log("Audio loaded: " .. audioClip.name)
        
        -- Play on AudioSource
        local audioSource = EAudio:GetAudioSource(someGameObject)
        if audioSource then
            audioSource.clip = audioClip
            audioSource:Play()
        end
    else
        Debug:LogError("Failed to load audio")
    end
end
```

## Supported Formats

### 3D Models
- ✅ **GLB** - Binary glTF format (recommended)

### Audio Files
- ✅ **OGG** - Ogg Vorbis (recommended, best compatibility)
- ✅ **WAV** - Uncompressed audio (larger files)
- ⚠️ **MP3** - Platform dependent support

## File Organization

Assets can be placed **anywhere inside your mod's root directory** using relative paths:
```
mod.io/
└── MyMod/
    ├── MyMod.config
    ├── Main.lua
    ├── myModel.glb          ← Root level works
    ├── sound.ogg            ← Root level works
    ├── EAssets/
    │   ├── Models/
    │   │   ├── character.glb
    │   │   ├── weapon.glb
    │   │   └── environment.glb
    │   └── Audio/
    │       ├── music.ogg
    │       ├── effects.wav
    │       └── voiceover.ogg
    ├── Resources/
    │   └── player.glb       ← Custom folders work
    └── Sounds/
        └── ambient/
            └── forest.ogg   ← Nested folders work
```

**Examples of valid paths:**
```lua
-- Root level files
EObject:LoadGLB("myModel.glb", "onModelLoaded", "MyMod")
EObject:LoadAudio("sound.ogg", "onAudioLoaded", "MyMod")

-- Organized in folders
EObject:LoadGLB("EAssets/Models/character.glb", "onCharacterLoaded", "MyMod")
EObject:LoadAudio("EAssets/Audio/music.ogg", "onMusicLoaded", "MyMod")

-- Custom organization
EObject:LoadGLB("Resources/player.glb", "onPlayerLoaded", "MyMod")
EObject:LoadAudio("Sounds/ambient/forest.ogg", "onForestLoaded", "MyMod")
```

## Complete Example

```lua
local loadedModel = nil
local backgroundMusic = nil
local audioSource = nil

function Start()
    -- Setup audio source
    local player = Engine:FindGameObject("Player")
    audioSource = EAudio:GetAudioSource(player)
    
    if not audioSource then
        Debug:LogError("No AudioSource found")
        return
    end
    
    -- Load 3D model
    EObject:LoadGLB("EAssets/Models/robot.glb", "onRobotLoaded", "MyMod")
    
    -- Load background music
    EObject:LoadAudio("EAssets/Audio/background.ogg", "onMusicLoaded", "MyMod")
    
    -- Load sound effect
    EObject:LoadAudio("EAssets/Audio/laser.wav", "onLaserLoaded", "MyMod")
end

function onRobotLoaded(gameObject)
    if gameObject then
        loadedModel = gameObject
        Debug:Log("Robot model loaded successfully!")
        
        -- Position the robot
        Engine:SetPosition(gameObject, 0, 0, 10)
        Engine:SetScale(gameObject, 1.5, 1.5, 1.5)
        
        -- Add physics
        local rigidbody = Engine:AddEngineComponent(gameObject, "Rigidbody")
        rigidbody.mass = 2.0
        
        -- Subscribe to events
        Engine:Subscribe(gameObject, "OnTriggerEnter", "MyMod", "onRobotTrigger")
    else
        Debug:LogError("Failed to load robot model")
    end
end

function onMusicLoaded(audioClip)
    if audioClip then
        backgroundMusic = audioClip
        Debug:Log("Background music loaded: " .. audioClip.name)
        Debug:Log("Duration: " .. audioClip.length .. " seconds")
        
        -- Play background music on loop
        audioSource.clip = audioClip
        audioSource.loop = true
        audioSource.volume = 0.3
        audioSource:Play()
    else
        Debug:LogError("Failed to load background music")
    end
end

function onLaserLoaded(audioClip)
    if audioClip then
        Debug:Log("Laser sound loaded: " .. audioClip.name)
        -- Store for later use in gameplay
        laserSoundEffect = audioClip
    else
        Debug:LogError("Failed to load laser sound")
    end
end

function onRobotTrigger(other)
    if other.name == "Player" then
        Debug:Log("Player touched the robot!")
        
        -- Play laser sound effect
        if laserSoundEffect then
            -- Create temporary AudioSource for sound effect
            local effectPlayer = Engine:CreateEmpty("LaserSound")
            local effectSource = Engine:AddEngineComponent(effectPlayer, "AudioSource")
            effectSource.clip = laserSoundEffect
            effectSource:Play()
            
            -- Destroy after sound finishes
            Engine:DestroyObject(effectPlayer, laserSoundEffect.length)
        end
    end
end

function OnUnloaded()
    -- Clean up loaded assets
    if loadedModel then
        Engine:DestroyObject(loadedModel)
    end
    
    -- Stop audio
    if audioSource then
        audioSource:Stop()
    end
end
```

## Notes

- **Async Loading**: All loading is non-blocking - the game continues while assets load
- **Relative Paths**: All paths are relative to your mod's root directory and can be placed anywhere inside it
- **Error Handling**: Always check if the loaded asset is not nil in callbacks
- **Memory Management**: GLB models automatically clean up when destroyed
- **Audio Formats**: Use OGG for best cross-platform compatibility
- **File Size**: Large assets will take longer to load - consider optimization
- **Callback Names**: Must be exact function names as strings
- **Mod Name**: Must match your mod's config name exactly

## AudioClip Properties
Once loaded, AudioClip objects have these properties:
- `audioClip.name` - Clip name
- `audioClip.length` - Duration in seconds
- `audioClip.samples` - Number of audio samples
- `audioClip.channels` - Number of audio channels (1=mono, 2=stereo)
- `audioClip.frequency` - Sample rate (e.g., 44100 Hz)
# Audio API

Audio control functions for Lua mods.

## Methods

**GetAudioSource(obj)** - Get AudioSource component
```lua
local audioSource = EAudio:GetAudioSource(player)
if audioSource then
    audioSource:Play()
    audioSource.volume = 0.8
end
```

**SetGlobalVolume(volume)** - Set global audio volume (0.0-1.0)
```lua
EAudio:SetGlobalVolume(0.5)
```

**GetGlobalVolume()** - Get current global volume
```lua
local volume = EAudio:GetGlobalVolume()
```

**SetGlobalPause(pause)** - Pause/unpause all audio
```lua
EAudio:SetGlobalPause(true)  -- Pause all
EAudio:SetGlobalPause(false) -- Resume all
```

**IsGlobalPaused()** - Check if audio is globally paused
```lua
if EAudio:IsGlobalPaused() then
    Debug:Log("Audio is paused")
end
```

**PlayClipAtPoint(clipName, x, y, z, volume)** - Play audio clip at world position
```lua
EAudio:PlayClipAtPoint("explosion", 10, 5, 0, 1.0)
```

**HasAudioSource(obj)** - Check if object has AudioSource
```lua
if EAudio:HasAudioSource(player) then
    Debug:Log("Player has audio")
end
```

## Example
```lua
function Start()
    local player = Engine:FindGameObject("Player")
    local audio = EAudio:GetAudioSource(player)
    
    if audio then
        audio.volume = 0.7
        audio.pitch = 1.2
        audio:Play()
    end
    
    EAudio:SetGlobalVolume(0.8)
end
```

## AudioSource Properties
Once you get an AudioSource, you can access its properties directly:
- `audioSource.volume` - Volume (0.0-1.0)
- `audioSource.pitch` - Pitch multiplier
- `audioSource.loop` - Loop the clip
- `audioSource.mute` - Mute the source
- `audioSource.isPlaying` - Check if playing
- `audioSource.time` - Current playback time
- `audioSource:Play()` - Start playing
- `audioSource:Stop()` - Stop playing
- `audioSource:Pause()` - Pause playback
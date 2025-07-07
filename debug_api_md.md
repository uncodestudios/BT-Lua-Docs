# Debug API

Logging functions for Lua mods.

## Methods

**Log(message)** - Log a message
```lua
Debug:Log("Hello World!")
```

**LogWarning(message)** - Log a warning
```lua
Debug:LogWarning("This is a warning")
```

**LogError(message)** - Log an error
```lua
Debug:LogError("Something went wrong!")
```

## Example
```lua
function Start()
    Debug:Log("Mod loaded")
end
```
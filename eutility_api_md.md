# Utility API

General utility functions for Lua mods.

## Random Functions

**RandomRange(min, max)** - Random float between min and max
```lua
local randomFloat = EUtility:RandomRange(1.0, 10.0)
```

**RandomRangeInt(min, max)** - Random integer between min and max (exclusive)
```lua
local randomInt = EUtility:RandomRangeInt(1, 6) -- Returns 1-5
```

**RandomValue()** - Random float between 0.0 and 1.0
```lua
local random = EUtility:RandomValue()
```

**SetRandomSeed(seed)** - Set random number seed
```lua
EUtility:SetRandomSeed(12345) -- Repeatable random sequence
```

**RandomBool()** - Random true/false
```lua
local coinFlip = EUtility:RandomBool()
```

**RandomNormal()** - Random float between -1.0 and 1.0
```lua
local randomDir = EUtility:RandomNormal()
```

## Cursor Control

**SetCursorVisible(visible)** - Show/hide cursor
```lua
EUtility:SetCursorVisible(false) -- Hide cursor
```

**IsCursorVisible()** - Check if cursor is visible
```lua
if EUtility:IsCursorVisible() then
    Debug:Log("Cursor is visible")
end
```

**SetCursorLocked(locked)** - Lock cursor to center of screen
```lua
EUtility:SetCursorLocked(true) -- Lock for FPS games
```

**IsCursorLocked()** - Check if cursor is locked
```lua
if EUtility:IsCursorLocked() then
    Debug:Log("Cursor is locked")
end
```

**SetCursorConfinedToWindow(confined)** - Keep cursor in game window
```lua
EUtility:SetCursorConfinedToWindow(true)
```

## Debug Drawing

**DrawLine(x1, y1, z1, x2, y2, z2, duration)** - Draw debug line
```lua
EUtility:DrawLine(0, 0, 0, 10, 10, 10, 2.0) -- White line for 2 seconds
```

**DrawLineColored(x1, y1, z1, x2, y2, z2, r, g, b, duration)** - Draw colored line
```lua
EUtility:DrawLineColored(0, 0, 0, 5, 0, 0, 1, 0, 0, 1.0) -- Red line
```

**DrawRay(x, y, z, dirX, dirY, dirZ, duration)** - Draw debug ray
```lua
EUtility:DrawRay(0, 0, 0, 1, 0, 0, 1.0) -- Ray pointing right
```

**DrawRayColored(x, y, z, dirX, dirY, dirZ, r, g, b, duration)** - Draw colored ray
```lua
EUtility:DrawRayColored(0, 0, 0, 0, 1, 0, 0, 1, 0, 2.0) -- Green ray up
```

**DrawLineBetweenObjects(obj1, obj2, duration)** - Draw line between objects
```lua
local player = Engine:FindGameObject("Player")
local enemy = Engine:FindGameObject("Enemy")
EUtility:DrawLineBetweenObjects(player, enemy, 1.0)
```

**DrawLineBetweenObjectsColored(obj1, obj2, r, g, b, duration)** - Colored line between objects
```lua
EUtility:DrawLineBetweenObjectsColored(player, enemy, 1, 0, 0, 1.0) -- Red line
```

## String Formatting

**FormatFloat(value, decimals)** - Format float to string with decimals
```lua
local formatted = EUtility:FormatFloat(3.14159, 2) -- Returns "3.14"
```

**FormatTime(seconds)** - Format seconds as MM:SS
```lua
local timeStr = EUtility:FormatTime(125) -- Returns "02:05"
```

**FormatTimeWithHours(seconds)** - Format seconds as HH:MM:SS
```lua
local timeStr = EUtility:FormatTimeWithHours(3665) -- Returns "01:01:05"
```

## String Parsing

**ParseFloat(value)** - Parse string to float
```lua
local number = EUtility:ParseFloat("3.14") -- Returns 3.14
```

**ParseInt(value)** - Parse string to integer
```lua
local number = EUtility:ParseInt("42") -- Returns 42
```

**ParseBool(value)** - Parse string to boolean
```lua
local bool = EUtility:ParseBool("true") -- Returns true
```

## Clipboard

**CopyToClipboard(text)** - Copy text to system clipboard
```lua
EUtility:CopyToClipboard("Hello World!")
```

**GetFromClipboard()** - Get text from system clipboard
```lua
local clipboardText = EUtility:GetFromClipboard()
```

## Screen Capture

**TakeScreenshot(filename)** - Take screenshot
```lua
EUtility:TakeScreenshot("screenshot.png")
```

## Screen Info

**GetScreenWidth()** - Get screen width in pixels
```lua
local width = EUtility:GetScreenWidth()
```

**GetScreenHeight()** - Get screen height in pixels
```lua
local height = EUtility:GetScreenHeight()
```

**GetScreenDPI()** - Get screen DPI
```lua
local dpi = EUtility:GetScreenDPI()
```

**IsFullscreen()** - Check if in fullscreen mode
```lua
if EUtility:IsFullscreen() then
    Debug:Log("Running in fullscreen")
end
```

**SetFullscreen(fullscreen)** - Set fullscreen mode
```lua
EUtility:SetFullscreen(true) -- Enable fullscreen
```

**SetResolution(width, height, fullscreen)** - Set screen resolution
```lua
EUtility:SetResolution(1920, 1080, true)
```

## Quality Settings

**SetQualityLevel(qualityLevel)** - Set graphics quality level
```lua
EUtility:SetQualityLevel(2) -- Set to medium quality
```

**GetQualityLevel()** - Get current quality level
```lua
local quality = EUtility:GetQualityLevel()
```

**GetQualityNames()** - Get array of quality level names
```lua
local qualityNames = EUtility:GetQualityNames()
for i, name in ipairs(qualityNames) do
    Debug:Log("Quality " .. i .. ": " .. name)
end
```

**SetMasterTextureLimit(limit)** - Set texture quality limit
```lua
EUtility:SetMasterTextureLimit(0) -- Full quality textures
```

**SetShadowDistance(distance)** - Set shadow render distance
```lua
EUtility:SetShadowDistance(50.0)
```

## Timing

**GetRealTimeSinceStartup()** - Get real time since game started
```lua
local realTime = EUtility:GetRealTimeSinceStartup()
```

**GetFrameCount()** - Get total frames rendered
```lua
local frames = EUtility:GetFrameCount()
```

**SetFixedDeltaTime(fixedDeltaTime)** - Set physics timestep
```lua
EUtility:SetFixedDeltaTime(0.02) -- 50 FPS physics
```

**SetMaximumDeltaTime(maximumDeltaTime)** - Set max frame time
```lua
EUtility:SetMaximumDeltaTime(0.1) -- Prevent huge time jumps
```

## Value Validation

**IsNaN(value)** - Check if value is Not a Number
```lua
if EUtility:IsNaN(someValue) then
    Debug:LogError("Invalid number!")
end
```

**IsInfinity(value)** - Check if value is infinite
```lua
if EUtility:IsInfinity(someValue) then
    Debug:LogWarning("Infinite value detected!")
end
```

## Object Utilities

**SetLayerMask(obj, layer)** - Set object layer
```lua
EUtility:SetLayerMask(player, 8) -- Set to layer 8
```

**GetLayerMask(obj)** - Get object layer
```lua
local layer = EUtility:GetLayerMask(enemy)
```

**SetTag(obj, tag)** - Set object tag
```lua
EUtility:SetTag(pickup, "Collectible")
```

**GetTag(obj)** - Get object tag
```lua
local tag = EUtility:GetTag(someObject)
```

**CompareTag(obj, tag)** - Compare object tag
```lua
if EUtility:CompareTag(hitObject, "Enemy") then
    Debug:Log("Hit an enemy!")
end
```

## Object Instantiation

**Instantiate(prefab, x, y, z)** - Create object instance
```lua
local prefab = Engine:FindGameObject("BulletPrefab")
EUtility:Instantiate(prefab, 0, 0, 10)
```

**InstantiateAndReturn(prefab, x, y, z)** - Create and return object instance
```lua
local newBullet = EUtility:InstantiateAndReturn(bulletPrefab, 0, 0, 10)
```

## Threading

**Wait(seconds)** - Block thread for time (use sparingly!)
```lua
EUtility:Wait(1.0) -- Sleep for 1 second - WARNING: Blocks game!
```

## Example
```lua
function Start()
    -- Setup cursor for FPS game
    EUtility:SetCursorLocked(true)
    EUtility:SetCursorVisible(false)
    
    -- Set random seed for consistent behavior
    EUtility:SetRandomSeed(12345)
    
    -- Set quality settings
    EUtility:SetQualityLevel(3)
    EUtility:SetShadowDistance(100.0)
    
    Debug:Log("Screen: " .. EUtility:GetScreenWidth() .. "x" .. EUtility:GetScreenHeight())
end

function Update()
    -- Random enemy spawning
    if EUtility:RandomValue() < 0.01 then -- 1% chance per frame
        local x = EUtility:RandomRange(-10, 10)
        local z = EUtility:RandomRange(-10, 10)
        local enemy = EUtility:InstantiateAndReturn(enemyPrefab, x, 0, z)
        EUtility:SetTag(enemy, "Enemy")
    end
    
    -- Debug drawing
    local player = Engine:FindGameObject("Player")
    if player then
        -- Draw forward direction
        local pos = player.transform.position
        local forward = player.transform.forward
        EUtility:DrawRayColored(pos.x, pos.y, pos.z, forward.x, forward.y, forward.z, 0, 1, 0, 0.1)
    end
    
    -- Screenshot on F12
    if EInput:GetKeyDown(KeyCode.F12) then
        local filename = "screenshot_" .. EUtility:GetFrameCount() .. ".png"
        EUtility:TakeScreenshot(filename)
        Debug:Log("Screenshot saved: " .. filename)
    end
    
    -- Toggle fullscreen on Alt+Enter
    if EInput:IsAltHeld() and EInput:IsEnterPressed() then
        EUtility:SetFullscreen(not EUtility:IsFullscreen())
    end
end
```

## Notes
- Debug drawing only visible in Scene view during development
- Wait() blocks the entire game thread - avoid using it
- Quality settings changes take effect immediately
- Screenshots are saved to the game's data folder
- Random functions use Unity's built-in random number generator
# Input API

Input handling functions for Lua mods.

## Keyboard Input

**GetKey(key)** - Check if key is held down
```lua
if EInput:GetKey("w") then
    -- Move forward while W is held
end
```

**GetKeyDown(key)** - Check if key was just pressed
```lua
if EInput:GetKeyDown("space") then
    -- Jump when space is pressed
end
```

**GetKeyUp(key)** - Check if key was just released
```lua
if EInput:GetKeyUp("space") then
    -- Stop jump when space is released
end
```

**GetKeyCode(keyCode)** - Check key by KeyCode number
```lua
if EInput:GetKeyCode(32) then -- Space = 32
    -- Space is held
end
```

**GetKeyCodeDown(keyCode)** - Check key down by KeyCode
```lua
if EInput:GetKeyCodeDown(32) then
    -- Space just pressed
end
```

**GetKeyCodeUp(keyCode)** - Check key up by KeyCode
```lua
if EInput:GetKeyCodeUp(32) then
    -- Space just released
end
```

## Mouse Input

**GetMouseButton(button)** - Check if mouse button is held (0=left, 1=right, 2=middle)
```lua
if EInput:GetMouseButton(0) then
    -- Left mouse button held
end
```

**GetMouseButtonDown(button)** - Check if mouse button was just pressed
```lua
if EInput:GetMouseButtonDown(0) then
    -- Left mouse button clicked
end
```

**GetMouseButtonUp(button)** - Check if mouse button was just released
```lua
if EInput:GetMouseButtonUp(0) then
    -- Left mouse button released
end
```

**GetMouseX()** - Get mouse X position
```lua
local mouseX = EInput:GetMouseX()
```

**GetMouseY()** - Get mouse Y position
```lua
local mouseY = EInput:GetMouseY()
```

**GetMouseScrollDelta()** - Get mouse scroll wheel delta
```lua
local scroll = EInput:GetMouseScrollDelta()
if scroll > 0 then
    -- Scrolled up
elseif scroll < 0 then
    -- Scrolled down
end
```

## Axes and Buttons

**GetAxis(axisName)** - Get smoothed axis input (-1 to 1)
```lua
local horizontal = EInput:GetAxis("Horizontal")
local vertical = EInput:GetAxis("Vertical")
```

**GetAxisRaw(axisName)** - Get raw axis input (-1, 0, or 1)
```lua
local horizontalRaw = EInput:GetAxisRaw("Horizontal")
local verticalRaw = EInput:GetAxisRaw("Vertical")
```

**GetButton(buttonName)** - Check if button is held
```lua
if EInput:GetButton("Fire1") then
    -- Fire button held
end
```

**GetButtonDown(buttonName)** - Check if button was just pressed
```lua
if EInput:GetButtonDown("Jump") then
    -- Jump button pressed
end
```

**GetButtonUp(buttonName)** - Check if button was just released
```lua
if EInput:GetButtonUp("Fire1") then
    -- Fire button released
end
```

## Touch Input

**GetTouchCount()** - Get number of active touches
```lua
local touchCount = EInput:GetTouchCount()
```

**GetTouchX(index)** - Get touch X position
```lua
if EInput:GetTouchCount() > 0 then
    local touchX = EInput:GetTouchX(0)
end
```

**GetTouchY(index)** - Get touch Y position
```lua
if EInput:GetTouchCount() > 0 then
    local touchY = EInput:GetTouchY(0)
end
```

**GetTouchPhase(index)** - Get touch phase (0=began, 1=moved, 2=stationary, 3=ended, 4=canceled)
```lua
if EInput:GetTouchCount() > 0 then
    local phase = EInput:GetTouchPhase(0)
    if phase == 0 then
        -- Touch began
    end
end
```

## Modifier Keys

**IsShiftHeld()** - Check if any Shift key is held
```lua
if EInput:IsShiftHeld() then
    -- Shift modifier active
end
```

**IsCtrlHeld()** - Check if any Ctrl key is held
```lua
if EInput:IsCtrlHeld() then
    -- Ctrl modifier active
end
```

**IsAltHeld()** - Check if any Alt key is held
```lua
if EInput:IsAltHeld() then
    -- Alt modifier active
end
```

## General Input

**AnyKey()** - Check if any key is currently held
```lua
if EInput:AnyKey() then
    -- Some key is pressed
end
```

**AnyKeyDown()** - Check if any key was just pressed
```lua
if EInput:AnyKeyDown() then
    -- Some key was just pressed
end
```

**GetInputString()** - Get typed characters this frame
```lua
local typed = EInput:GetInputString()
if typed ~= "" then
    Debug:Log("Typed: " .. typed)
end
```

## Controller/Joystick

**IsDeviceConnected(deviceName)** - Check if input device is connected
```lua
if EInput:IsDeviceConnected("Controller") then
    -- Controller is connected
end
```

**GetJoystickNames()** - Get array of connected joystick names
```lua
local joysticks = EInput:GetJoystickNames()
for i, name in ipairs(joysticks) do
    Debug:Log("Joystick " .. i .. ": " .. name)
end
```

## Convenience Functions

**GetHorizontal()** - Get horizontal input (-1 to 1)
```lua
local horizontal = EInput:GetHorizontal() -- Same as GetAxis("Horizontal")
```

**GetVertical()** - Get vertical input (-1 to 1)
```lua
local vertical = EInput:GetVertical() -- Same as GetAxis("Vertical")
```

**GetHorizontalRaw()** - Get raw horizontal input (-1, 0, or 1)
```lua
local horizontalRaw = EInput:GetHorizontalRaw()
```

**GetVerticalRaw()** - Get raw vertical input (-1, 0, or 1)
```lua
local verticalRaw = EInput:GetVerticalRaw()
```

## Specific Key Checks

**IsEscapePressed()** - Check if Escape was pressed
```lua
if EInput:IsEscapePressed() then
    -- Open menu
end
```

**IsEnterPressed()** - Check if Enter was pressed
```lua
if EInput:IsEnterPressed() then
    -- Confirm action
end
```

**IsSpacePressed()** - Check if Space was pressed
```lua
if EInput:IsSpacePressed() then
    -- Space action
end
```

## WASD Keys

**IsWPressed()** - Check if W is held
```lua
if EInput:IsWPressed() then
    -- Move forward
end
```

**IsAPressed()** - Check if A is held
```lua
if EInput:IsAPressed() then
    -- Move left
end
```

**IsSPressed()** - Check if S is held
```lua
if EInput:IsSPressed() then
    -- Move backward
end
```

**IsDPressed()** - Check if D is held
```lua
if EInput:IsDPressed() then
    -- Move right
end
```

## Arrow Keys

**IsUpArrow()** - Check if Up arrow is held
```lua
if EInput:IsUpArrow() then
    -- Up arrow pressed
end
```

**IsDownArrow()** - Check if Down arrow is held
```lua
if EInput:IsDownArrow() then
    -- Down arrow pressed
end
```

**IsLeftArrow()** - Check if Left arrow is held
```lua
if EInput:IsLeftArrow() then
    -- Left arrow pressed
end
```

**IsRightArrow()** - Check if Right arrow is held
```lua
if EInput:IsRightArrow() then
    -- Right arrow pressed
end
```

## VR Input (hand: 0=left, 1=right)

**GetVRGripButtonDown(hand)** - Check if VR grip was pressed
```lua
if EInput:GetVRGripButtonDown(0) then -- Left hand
    -- Left grip pressed
end
```

**GetVRTriggerButtonDown(hand)** - Check if VR trigger was pressed
```lua
if EInput:GetVRTriggerButtonDown(1) then -- Right hand
    -- Right trigger pressed
end
```

**GetVRTriggerButtonTouched(hand)** - Check if VR trigger is touched
```lua
if EInput:GetVRTriggerButtonTouched(0) then
    -- Left trigger touched
end
```

**GetVRGripButtonFloat(hand)** - Get VR grip pressure (0.0 to 1.0)
```lua
local leftGrip = EInput:GetVRGripButtonFloat(0)
```

**GetVRTriggerButtonFloat(hand)** - Get VR trigger pressure (0.0 to 1.0)
```lua
local rightTrigger = EInput:GetVRTriggerButtonFloat(1)
```

**GetVRPrimaryButtonDown(hand)** - Check if VR primary button pressed
```lua
if EInput:GetVRPrimaryButtonDown(0) then
    -- Left primary button pressed
end
```

**GetVRSecondaryButtonDown(hand)** - Check if VR secondary button pressed
```lua
if EInput:GetVRSecondaryButtonDown(1) then
    -- Right secondary button pressed
end
```

**GetVRThumbStickX(hand)** - Get VR thumbstick X axis (-1 to 1)
```lua
local stickX = EInput:GetVRThumbStickX(0)
```

**GetVRThumbStickY(hand)** - Get VR thumbstick Y axis (-1 to 1)
```lua
local stickY = EInput:GetVRThumbStickY(1)
```

**GetVRDeviceVelocityX/Y/Z(hand)** - Get VR controller velocity
```lua
local velX = EInput:GetVRDeviceVelocityX(0)
local velY = EInput:GetVRDeviceVelocityY(0) 
local velZ = EInput:GetVRDeviceVelocityZ(0)
```

## Example
```lua
function Update()
    -- Basic movement
    local horizontal = EInput:GetHorizontal()
    local vertical = EInput:GetVertical()
    
    if horizontal ~= 0 or vertical ~= 0 then
        -- Move player
        local player = Engine:FindGameObject("Player")
        Engine:Translate(player, horizontal * 5 * ETime.DeltaTime, 0, vertical * 5 * ETime.DeltaTime)
    end
    
    -- Jump
    if EInput:IsJumping() then
        local player = Engine:FindGameObject("Player")
        local rb = EPhysics:GetRigidbody(player)
        if rb then
            rb:AddForce(Engine:CreateVector3(0, 10, 0))
        end
    end
    
    -- Fire weapon
    if EInput:GetMouseButtonDown(0) then
        Debug:Log("Weapon fired!")
    end
    
    -- Pause menu
    if EInput:IsEscapePressed() then
        Debug:Log("Opening pause menu")
    end
end
```
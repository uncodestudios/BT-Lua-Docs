# GUI API

Immediate mode GUI functions for Lua mods.

## Basic Controls

**Label(x, y, width, height, text)** - Display text label
```lua
EGUI:Label(10, 10, 200, 30, "Hello World!")
```

**Button(x, y, width, height, text)** - Interactive button
```lua
if EGUI:Button(10, 50, 100, 30, "Click Me!") then
    Debug:Log("Button clicked!")
end
```

**TextField(x, y, width, height, text)** - Single line text input
```lua
local inputText = EGUI:TextField(10, 100, 200, 30, currentText)
```

**TextArea(x, y, width, height, text)** - Multi-line text input
```lua
local description = EGUI:TextArea(10, 150, 300, 100, currentDescription)
```

**Toggle(x, y, width, height, value, text)** - Checkbox toggle
```lua
local isEnabled = EGUI:Toggle(10, 200, 150, 30, currentValue, "Enable Feature")
```

**Box(x, y, width, height, text)** - Background box with text
```lua
EGUI:Box(5, 5, 310, 250, "Settings Panel")
```

## Sliders

**HorizontalSlider(x, y, width, height, value, leftValue, rightValue)** - Horizontal slider
```lua
local volume = EGUI:HorizontalSlider(10, 250, 200, 20, currentVolume, 0.0, 1.0)
```

**VerticalSlider(x, y, width, height, value, topValue, bottomValue)** - Vertical slider
```lua
local brightness = EGUI:VerticalSlider(250, 50, 20, 200, currentBrightness, 1.0, 0.0)
```

## Selection Controls

**SelectionGrid(x, y, width, height, selected, texts, xCount)** - Grid selection
```lua
local options = {"Option 1", "Option 2", "Option 3", "Option 4"}
local selected = EGUI:SelectionGrid(10, 280, 300, 60, currentSelection, options, 2)
```

**Toolbar(x, y, width, height, selected, texts)** - Horizontal toolbar
```lua
local tabs = {"Home", "Settings", "About"}
local activeTab = EGUI:Toolbar(10, 350, 300, 30, currentTab, tabs)
```

## Scrollbars

**HorizontalScrollbar(x, y, width, height, value, size, leftValue, rightValue)** - Horizontal scrollbar
```lua
local scrollX = EGUI:HorizontalScrollbar(10, 400, 200, 20, currentScrollX, 0.1, 0.0, 1.0)
```

**VerticalScrollbar(x, y, width, height, value, size, topValue, bottomValue)** - Vertical scrollbar
```lua
local scrollY = EGUI:VerticalScrollbar(280, 50, 20, 200, currentScrollY, 0.1, 0.0, 1.0)
```

## Windows

**Window(id, x, y, width, height, title)** - Basic window
```lua
EGUI:Window(1, 100, 100, 300, 200, "My Window")
```

**DraggableWindow(id, x, y, width, height, title)** - Draggable window
```lua
EGUI:DraggableWindow(2, windowX, windowY, 300, 200, "Draggable Window")
```

**SetWindowRect(id, x, y, width, height)** - Set window position/size
```lua
EGUI:SetWindowRect(2, 150, 150, 300, 200)
```

**GetWindowX(id)** - Get window X position
```lua
local x = EGUI:GetWindowX(2)
```

**GetWindowY(id)** - Get window Y position
```lua
local y = EGUI:GetWindowY(2)
```

**DragWindow()** - Make current window draggable (call inside window)
```lua
EGUI:DragWindow()
```

## Screen Information

**GetScreenWidth()** - Get screen width
```lua
local screenWidth = EGUI:GetScreenWidth()
```

**GetScreenHeight()** - Get screen height
```lua
local screenHeight = EGUI:GetScreenHeight()
```

**GetMouseX()** - Get mouse X position
```lua
local mouseX = EGUI:GetMouseX()
```

**GetMouseY()** - Get mouse Y position (GUI coordinates)
```lua
local mouseY = EGUI:GetMouseY()
```

## Color Control

**SetColor(r, g, b, a)** - Set GUI tint color
```lua
EGUI:SetColor(1.0, 0.5, 0.5, 1.0) -- Reddish tint
```

**SetBackgroundColor(r, g, b, a)** - Set background color
```lua
EGUI:SetBackgroundColor(0.2, 0.2, 0.8, 1.0) -- Blue background
```

**SetContentColor(r, g, b, a)** - Set content (text) color
```lua
EGUI:SetContentColor(1.0, 1.0, 0.0, 1.0) -- Yellow text
```

**ResetColor()** - Reset GUI color to white
```lua
EGUI:ResetColor()
```

**ResetBackgroundColor()** - Reset background color to white
```lua
EGUI:ResetBackgroundColor()
```

**ResetContentColor()** - Reset content color to white
```lua
EGUI:ResetContentColor()
```

## Example
```lua
local windowRect = { x = 10, y = 10, width = 300, height = 400 }
local playerName = "Player"
local health = 50
local showDebug = false

function OnGUI()
    -- Background box
    EGUI:Box(windowRect.x, windowRect.y, windowRect.width, windowRect.height, "Game Settings")
    
    -- Player name input
    EGUI:Label(windowRect.x + 10, windowRect.y + 30, 280, 20, "Player Name:")
    playerName = EGUI:TextField(windowRect.x + 10, windowRect.y + 50, 280, 30, playerName)
    
    -- Health slider
    EGUI:Label(windowRect.x + 10, windowRect.y + 90, 280, 20, "Health: " .. health)
    health = EGUI:HorizontalSlider(windowRect.x + 10, windowRect.y + 110, 280, 20, health, 0, 100)
    
    -- Debug toggle
    showDebug = EGUI:Toggle(windowRect.x + 10, windowRect.y + 140, 200, 30, showDebug, "Show Debug Info")
    
    -- Apply button
    if EGUI:Button(windowRect.x + 10, windowRect.y + 180, 100, 30, "Apply") then
        Debug:Log("Settings applied!")
        Debug:Log("Name: " .. playerName .. ", Health: " .. health)
    end
    
    -- Reset button
    if EGUI:Button(windowRect.x + 120, windowRect.y + 180, 100, 30, "Reset") then
        playerName = "Player"
        health = 100
        showDebug = false
    end
    
    -- Color example
    EGUI:SetContentColor(1.0, 0.5, 0.5, 1.0)
    EGUI:Label(windowRect.x + 10, windowRect.y + 220, 280, 20, "This text is red!")
    EGUI:ResetContentColor()
end
```

## Notes
- All GUI functions must be called from an `OnGUI()` function
- Coordinates are in screen pixels (0,0 = top-left)
- Colors use RGBA values from 0.0 to 1.0
- GUI is drawn every frame, so store state in variables outside OnGUI()
- Use unique window IDs to avoid conflicts between mods
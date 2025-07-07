# Math API

Mathematical functions for Lua mods.

## Basic Math

**Abs(value)** - Absolute value
```lua
local distance = EMath:Abs(-5.5) -- Returns 5.5
```

**Sqrt(value)** - Square root
```lua
local result = EMath:Sqrt(16) -- Returns 4
```

**Pow(value, power)** - Power/exponentiation
```lua
local result = EMath:Pow(2, 3) -- Returns 8 (2^3)
```

**Sign(value)** - Sign of number (-1, 0, or 1)
```lua
local sign = EMath:Sign(-42) -- Returns -1
```

## Trigonometry

**Sin(radians)** - Sine
```lua
local result = EMath:Sin(EMath:PI() / 2) -- Returns 1
```

**Cos(radians)** - Cosine
```lua
local result = EMath:Cos(0) -- Returns 1
```

**Tan(radians)** - Tangent
```lua
local result = EMath:Tan(EMath:PI() / 4) -- Returns 1
```

**Asin(value)** - Arc sine (inverse sine)
```lua
local angle = EMath:Asin(1) -- Returns PI/2
```

**Acos(value)** - Arc cosine (inverse cosine)
```lua
local angle = EMath:Acos(0) -- Returns PI/2
```

**Atan(value)** - Arc tangent (inverse tangent)
```lua
local angle = EMath:Atan(1) -- Returns PI/4
```

**Atan2(y, x)** - Two-argument arc tangent
```lua
local angle = EMath:Atan2(1, 1) -- Returns PI/4
```

## Angle Conversion

**DegToRad(degrees)** - Convert degrees to radians
```lua
local radians = EMath:DegToRad(90) -- Returns PI/2
```

**RadToDeg(radians)** - Convert radians to degrees
```lua
local degrees = EMath:RadToDeg(EMath:PI()) -- Returns 180
```

**LerpAngle(a, b, t)** - Interpolate between angles
```lua
local angle = EMath:LerpAngle(0, 90, 0.5) -- Returns 45
```

**DeltaAngle(current, target)** - Shortest angle difference
```lua
local diff = EMath:DeltaAngle(350, 10) -- Returns 20 (not 340)
```

## Min/Max and Clamping

**Min(a, b)** - Minimum of two values
```lua
local smaller = EMath:Min(5, 10) -- Returns 5
```

**Max(a, b)** - Maximum of two values
```lua
local larger = EMath:Max(5, 10) -- Returns 10
```

**Clamp(value, min, max)** - Clamp value between min and max
```lua
local clamped = EMath:Clamp(15, 0, 10) -- Returns 10
```

**Clamp01(value)** - Clamp value between 0 and 1
```lua
local normalized = EMath:Clamp01(1.5) -- Returns 1
```

## Interpolation

**Lerp(a, b, t)** - Linear interpolation (t clamped 0-1)
```lua
local result = EMath:Lerp(0, 100, 0.5) -- Returns 50
```

**LerpUnclamped(a, b, t)** - Linear interpolation (t not clamped)
```lua
local result = EMath:LerpUnclamped(0, 100, 1.5) -- Returns 150
```

**InverseLerp(a, b, value)** - Get t value for lerp
```lua
local t = EMath:InverseLerp(0, 100, 25) -- Returns 0.25
```

**SmoothStep(from, to, t)** - Smooth interpolation
```lua
local smooth = EMath:SmoothStep(0, 1, 0.5) -- Smoother than Lerp
```

**MoveTowards(current, target, maxDelta)** - Move towards target by max amount
```lua
local newPos = EMath:MoveTowards(10, 20, 3) -- Returns 13
```

## Repeating Functions

**PingPong(t, length)** - Ping-pong between 0 and length
```lua
local value = EMath:PingPong(3.5, 2) -- Returns 0.5 (bounces back)
```

**Repeat(t, length)** - Repeat value in range 0 to length
```lua
local value = EMath:Repeat(7, 3) -- Returns 1 (7 % 3)
```

## Rounding

**Round(value)** - Round to nearest integer
```lua
local rounded = EMath:Round(3.7) -- Returns 4
```

**RoundToInt(value)** - Round to nearest integer (returns int)
```lua
local rounded = EMath:RoundToInt(3.7) -- Returns 4
```

**Floor(value)** - Round down
```lua
local floored = EMath:Floor(3.7) -- Returns 3
```

**FloorToInt(value)** - Round down (returns int)
```lua
local floored = EMath:FloorToInt(3.7) -- Returns 3
```

**Ceil(value)** - Round up
```lua
local ceiled = EMath:Ceil(3.2) -- Returns 4
```

**CeilToInt(value)** - Round up (returns int)
```lua
local ceiled = EMath:CeilToInt(3.2) -- Returns 4
```

## Logarithms and Exponentials

**Log(value)** - Natural logarithm
```lua
local result = EMath:Log(EMath:Exp(1)) -- Returns 1
```

**Log10(value)** - Base-10 logarithm
```lua
local result = EMath:Log10(100) -- Returns 2
```

**Exp(value)** - Exponential (e^value)
```lua
local result = EMath:Exp(1) -- Returns e (~2.718)
```

## Vector Math

**Distance(x1, y1, x2, y2)** - 2D distance
```lua
local dist = EMath:Distance(0, 0, 3, 4) -- Returns 5
```

**Distance3D(x1, y1, z1, x2, y2, z2)** - 3D distance
```lua
local dist = EMath:Distance3D(0, 0, 0, 1, 1, 1) -- Returns sqrt(3)
```

**Magnitude(x, y)** - 2D vector magnitude
```lua
local mag = EMath:Magnitude(3, 4) -- Returns 5
```

**Magnitude3D(x, y, z)** - 3D vector magnitude
```lua
local mag = EMath:Magnitude3D(1, 1, 1) -- Returns sqrt(3)
```

**Dot(x1, y1, x2, y2)** - 2D dot product
```lua
local dot = EMath:Dot(1, 0, 0, 1) -- Returns 0
```

**Dot3D(x1, y1, z1, x2, y2, z2)** - 3D dot product
```lua
local dot = EMath:Dot3D(1, 0, 0, 1, 0, 0) -- Returns 1
```

**Angle(x1, y1, x2, y2)** - Angle between 2D vectors (degrees)
```lua
local angle = EMath:Angle(1, 0, 0, 1) -- Returns 90
```

**Angle3D(x1, y1, z1, x2, y2, z2)** - Angle between 3D vectors (degrees)
```lua
local angle = EMath:Angle3D(1, 0, 0, 0, 1, 0) -- Returns 90
```

## Constants

**PI()** - Pi constant
```lua
local pi = EMath:PI() -- Returns 3.14159...
```

**Infinity()** - Positive infinity
```lua
local inf = EMath:Infinity()
```

**NegativeInfinity()** - Negative infinity
```lua
local negInf = EMath:NegativeInfinity()
```

**Epsilon()** - Smallest float value
```lua
local epsilon = EMath:Epsilon()
```

## Example
```lua
function Update()
    local time = ETime.Time
    
    -- Oscillating movement using sine wave
    local player = Engine:FindGameObject("Player")
    if player then
        local x = EMath:Sin(time) * 5
        local y = EMath:Cos(time * 2) * 3
        Engine:SetPosition(player, x, y, 0)
    end
    
    -- Smooth camera follow
    local camera = Engine:FindGameObject("Main Camera")
    local target = Engine:FindGameObject("Player")
    if camera and target then
        local currentPos = camera.transform.position
        local targetPos = target.transform.position
        
        -- Lerp camera towards target
        local newX = EMath:Lerp(currentPos.x, targetPos.x, 2 * ETime.DeltaTime)
        local newY = EMath:Lerp(currentPos.y, targetPos.y, 2 * ETime.DeltaTime)
        Engine:SetPosition(camera, newX, newY, currentPos.z)
    end
    
    -- Distance check
    local enemy = Engine:FindGameObject("Enemy")
    if player and enemy then
        local dist = Engine:Distance(player, enemy)
        if dist < 5 then
            Debug:Log("Enemy nearby! Distance: " .. EMath:Round(dist))
        end
    end
end
```
# Physics API

Physics functions for Lua mods.

## Rigidbody Access

**GetRigidbody(obj)** - Get Rigidbody component
```lua
local player = Engine:FindGameObject("Player")
local rb = EPhysics:GetRigidbody(player)
if rb then
    rb.mass = 2.0
    rb.linearVelocity = Engine:CreateVector3(0, 10, 0)
end
```

**HasRigidbody(obj)** - Check if object has Rigidbody
```lua
if EPhysics:HasRigidbody(player) then
    Debug:Log("Player has physics")
end
```

## Raycasting

**Raycast(x, y, z, dirX, dirY, dirZ, distance)** - Check if ray hits anything
```lua
local hit = EPhysics:Raycast(0, 10, 0, 0, -1, 0, 20)
if hit then
    Debug:Log("Ground detected below player")
end
```

**RaycastHit(x, y, z, dirX, dirY, dirZ, distance)** - Get object hit by ray
```lua
local hitObject = EPhysics:RaycastHit(0, 10, 0, 0, -1, 0, 20)
if hitObject then
    Debug:Log("Hit object: " .. hitObject.name)
end
```

## Global Physics

**SetGravity(x, y, z)** - Set world gravity
```lua
EPhysics:SetGravity(0, -20, 0) -- Double gravity
EPhysics:SetGravity(0, 0, 0)   -- Zero gravity
```

**GetGravity()** - Get current gravity
```lua
local gravity = EPhysics:GetGravity()
Debug:Log("Gravity Y: " .. gravity.y)
```

## Constraints

**FreezePosition(obj, x, y, z)** - Freeze position axes
```lua
-- Freeze X and Z, allow Y movement
EPhysics:FreezePosition(player, true, false, true)
```

**FreezeRotation(obj, x, y, z)** - Freeze rotation axes
```lua
-- Freeze X and Z rotation, allow Y rotation
EPhysics:FreezeRotation(player, true, false, true)
```

## Example
```lua
function Start()
    local cube = Engine:CreateCube()
    Engine:SetPosition(cube, 0, 10, 0)
    
    -- Add physics
    local rb = Engine:AddEngineComponent(cube, "Rigidbody")
    rb.mass = 2.0
    rb.useGravity = true
    
    -- Check for ground
    local hitGround = EPhysics:Raycast(0, 10, 0, 0, -1, 0, 15)
    if hitGround then
        Debug:Log("Ground detected below cube")
    end
    
    -- Freeze rotation
    EPhysics:FreezeRotation(cube, true, true, true)
end

function Update()
    local player = Engine:FindGameObject("Player")
    if player then
        local rb = EPhysics:GetRigidbody(player)
        if rb then
            -- Apply force when space is pressed
            if EInput:GetKeyDown("space") then
                rb:AddForce(Engine:CreateVector3(0, 500, 0))
            end
            
            -- Movement with physics
            local horizontal = EInput:GetHorizontal()
            if horizontal ~= 0 then
                rb:AddForce(Engine:CreateVector3(horizontal * 10, 0, 0))
            end
        end
    end
end
```

## Rigidbody Properties
Once you get a Rigidbody, you can access its properties directly:
- `rb.mass` - Object mass
- `rb.linearVelocity` - Current velocity (Vector3)
- `rb.angularVelocity` - Current angular velocity (Vector3)
- `rb.linearDamping` - Linear drag
- `rb.angularDamping` - Angular drag
- `rb.useGravity` - Affected by gravity
- `rb.isKinematic` - Kinematic mode
- `rb.freezeRotation` - Freeze all rotation
- `rb.constraints` - Movement constraints
- `rb:AddForce(force)` - Add force
- `rb:AddTorque(torque)` - Add rotational force
- `rb:AddForceAtPosition(force, position)` - Add force at position
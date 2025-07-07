# Engine API

Core engine functions for Lua mods.

## Object Creation

**CreateVector3(x, y, z)** - Create a Vector3
```lua
local pos = Engine:CreateVector3(10, 5, 0)
```

**CreateQuaternion(x, y, z, w)** - Create a Quaternion
```lua
local rot = Engine:CreateQuaternion(0, 0, 0, 1)
```

**CreateCube()** - Create a cube primitive
```lua
local cube = Engine:CreateCube()
```

**CreateSphere()** - Create a sphere primitive
```lua
local sphere = Engine:CreateSphere()
```

**CreateCapsule()** - Create a capsule primitive
```lua
local capsule = Engine:CreateCapsule()
```

**CreateCylinder()** - Create a cylinder primitive
```lua
local cylinder = Engine:CreateCylinder()
```

**CreatePlane()** - Create a plane primitive
```lua
local plane = Engine:CreatePlane()
```

**CreateQuad()** - Create a quad primitive
```lua
local quad = Engine:CreateQuad()
```

**CreateEmpty(name)** - Create an empty GameObject
```lua
local empty = Engine:CreateEmpty("MyObject")
```

## Object Finding

**FindGameObject(name)** - Find GameObject by name
```lua
local player = Engine:FindGameObject("Player")
```

**FindGameObjectWithTag(tag)** - Find first GameObject with tag
```lua
local enemy = Engine:FindGameObjectWithTag("Enemy")
```

**FindGameObjectsWithTag(tag)** - Find all GameObjects with tag
```lua
local enemies = Engine:FindGameObjectsWithTag("Enemy")
```

**FindObjectOfEngineType(componentName)** - Find object with Unity component
```lua
local cameraObj = Engine:FindObjectOfEngineType("Camera")
```

**FindObjectOfCustomType(fullTypeName)** - Find object with custom component
```lua
local playerObj = Engine:FindObjectOfCustomType("MyNamespace.PlayerController")
```

## Object Management

**DestroyObject(obj)** - Destroy a GameObject
```lua
Engine:DestroyObject(someObject)
```

## Transform Operations

**SetPosition(obj, x, y, z)** - Set world position
```lua
Engine:SetPosition(player, 10, 0, 5)
```

**SetLocalPosition(obj, x, y, z)** - Set local position
```lua
Engine:SetLocalPosition(child, 1, 2, 3)
```

**SetRotation(obj, x, y, z, w)** - Set rotation (quaternion)
```lua
Engine:SetRotation(player, 0, 0, 0, 1)
```

**SetEulerAngles(obj, x, y, z)** - Set rotation (euler angles)
```lua
Engine:SetEulerAngles(player, 0, 90, 0)
```

**SetScale(obj, x, y, z)** - Set local scale
```lua
Engine:SetScale(cube, 2, 2, 2)
```

**Translate(obj, x, y, z)** - Move object relative to current position
```lua
Engine:Translate(player, 0, 0, 1) -- Move forward
```

**Rotate(obj, x, y, z)** - Rotate object relative to current rotation
```lua
Engine:Rotate(player, 0, 45, 0) -- Turn 45 degrees
```

**RotateAround(obj, pivotX, pivotY, pivotZ, axisX, axisY, axisZ, angle)** - Rotate around point
```lua
Engine:RotateAround(planet, 0, 0, 0, 0, 1, 0, 90)
```

**LookAt(obj, target)** - Make object look at target
```lua
Engine:LookAt(camera, player)
```

**LookAtPosition(obj, x, y, z)** - Make object look at position
```lua
Engine:LookAtPosition(turret, 10, 0, 5)
```

## Component Management

**AddEngineComponent(obj, componentName)** - Add Unity component
```lua
local rigidbody = Engine:AddEngineComponent(cube, "Rigidbody")
local collider = Engine:AddEngineComponent(cube, "BoxCollider")
```

**AddCustomComponent(obj, fullTypeName)** - Add custom component
```lua
local controller = Engine:AddCustomComponent(player, "MyGame.PlayerController")
```

**GetEngineComponent(obj, componentName)** - Get Unity component
```lua
local rigidbody = Engine:GetEngineComponent(player, "Rigidbody")
```

**GetCustomComponent(obj, fullTypeName)** - Get custom component
```lua
local controller = Engine:GetCustomComponent(player, "MyGame.PlayerController")
```

**HasEngineComponent(obj, componentName)** - Check for Unity component
```lua
if Engine:HasEngineComponent(player, "Rigidbody") then
    Debug:Log("Player has physics")
end
```

**HasCustomComponent(obj, fullTypeName)** - Check for custom component
```lua
if Engine:HasCustomComponent(player, "MyGame.PlayerController") then
    Debug:Log("Player has controller")
end
```

**SetComponentValue(component, fieldName, value)** - Set component field
```lua
local light = Engine:GetEngineComponent(lamp, "Light")
Engine:SetComponentValue(light, "intensity", 2.0)
```

**SetComponentFloat(component, fieldName, value)** - Set component float field
```lua
Engine:SetComponentFloat(light, "range", 10.0)
```

## Utility Functions

**Distance(obj1, obj2)** - Distance between two objects
```lua
local dist = Engine:Distance(player, enemy)
```

**DistanceToPosition(obj, x, y, z)** - Distance to position
```lua
local dist = Engine:DistanceToPosition(player, 0, 0, 0)
```

## Input Functions

**GetKey(key)** - Check if key is held
```lua
if Engine:GetKey("w") then
    -- Move forward
end
```

**GetKeyDown(key)** - Check if key was just pressed
```lua
if Engine:GetKeyDown("space") then
    -- Jump
end
```

**GetKeyUp(key)** - Check if key was just released
```lua
if Engine:GetKeyUp("space") then
    -- Stop jumping
end
```

**GetMouseButton(button)** - Check if mouse button is held (0=left, 1=right, 2=middle)
```lua
if Engine:GetMouseButton(0) then
    -- Left mouse held
end
```

**GetMouseButtonDown(button)** - Check if mouse button was just pressed
```lua
if Engine:GetMouseButtonDown(0) then
    -- Left mouse clicked
end
```

**GetMouseButtonUp(button)** - Check if mouse button was just released
```lua
if Engine:GetMouseButtonUp(0) then
    -- Left mouse released
end
```

## Event Subscription

**Subscribe(obj, eventType, modName, luaFunctionName)** - Subscribe to Unity events
```lua
Engine:Subscribe(player, "OnTriggerEnter", "MyMod", "OnPlayerTrigger")
```

**Unsubscribe(obj, eventType, modName, luaFunctionName)** - Unsubscribe from events
```lua
Engine:Unsubscribe(player, "OnTriggerEnter", "MyMod", "OnPlayerTrigger")
```

**UnsubscribeAll(obj, modName)** - Remove all subscriptions for a mod
```lua
Engine:UnsubscribeAll(player, "MyMod")
```

**GetSubscribedEvents(obj)** - Get list of subscribed events
```lua
local events = Engine:GetSubscribedEvents(player)
```

**GetSubscriptionCount(obj)** - Get number of subscriptions
```lua
local count = Engine:GetSubscriptionCount(player)
```

## Example
```lua
function Start()
    -- Create objects
    local cube = Engine:CreateCube()
    local pos = Engine:CreateVector3(0, 5, 0)
    
    -- Set properties
    cube.name = "MyCube"
    cube.tag = "Interactive"
    Engine:SetPosition(cube, 0, 5, 0)
    
    -- Add components
    local rb = Engine:AddEngineComponent(cube, "Rigidbody")
    rb.mass = 2.0
    
    -- Subscribe to events
    Engine:Subscribe(cube, "OnTriggerEnter", "MyMod", "OnCubeTrigger")
end

function OnCubeTrigger(other)
    Debug:Log("Cube triggered by: " .. other.name)
end
```

## GameObject Properties
Once you have a GameObject, you can access its properties directly:
- `obj.name` - Object name
- `obj.tag` - Object tag
- `obj.transform` - Transform component
- `obj.activeInHierarchy` - Is active in scene
- `obj:SetActive(true/false)` - Enable/disable object

## Transform Properties
Access transform properties directly:
- `transform.position` - World position (Vector3)
- `transform.localPosition` - Local position (Vector3)
- `transform.rotation` - Rotation (Quaternion)
- `transform.eulerAngles` - Euler angles (Vector3)
- `transform.localScale` - Local scale (Vector3)
- `transform.forward` - Forward direction (Vector3)
- `transform.right` - Right direction (Vector3)
- `transform.up` - Up direction (Vector3)
- `transform.parent` - Parent transform
- `transform.childCount` - Number of children
- `transform:GetChild(index)` - Get child by index

## Vector3 Properties
Vector3 objects have these properties:
- `vector.x` - X component
- `vector.y` - Y component  
- `vector.z` - Z component
- `vector.magnitude` - Length of vector
- `vector.normalized` - Normalized vector
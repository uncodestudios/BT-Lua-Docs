# Complete Lua Modding API Documentation

## Table of Contents
1. [Debug (Logging)](#debug-logging)
2. [Engine (Core GameObject Operations)](#engine-core-gameobject-operations)
3. [ETime (Time Functions)](#etime-time-functions)
4. [EGUI (User Interface)](#egui-user-interface)
5. [EInput (Input Handling)](#einput-input-handling)
6. [EPhysics (Physics Operations)](#ephysics-physics-operations)
7. [EAudio (Audio Control)](#eaudio-audio-control)
8. [EScene (Scene Management)](#escene-scene-management)
9. [EMath (Math Utilities)](#emath-math-utilities)
10. [EUtility (General Utilities)](#eutility-general-utilities)
11. [Lifecycle Functions](#lifecycle-functions)

---

## Debug (Logging)

### Debug:Log(message)
Log a message to console.
```lua
Debug:Log("Player health: " .. playerHealth)
```

### Debug:LogWarning(message)
Log a warning message.
```lua
Debug:LogWarning("Player health is low!")
```

### Debug:LogError(message)
Log an error message.
```lua
Debug:LogError("Failed to load save file!")
```

---

## Engine (Core GameObject Operations)

### Finding Objects

#### Engine:FindGameObject(name)
Find a GameObject by name.
```lua
local player = Engine:FindGameObject("Player")
```

#### Engine:FindGameObjectWithTag(tag)
Find first GameObject with tag.
```lua
local enemy = Engine:FindGameObjectWithTag("Enemy")
```

#### Engine:FindGameObjectsWithTag(tag)
Find all GameObjects with tag.
```lua
local enemies = Engine:FindGameObjectsWithTag("Enemy")
```

#### Engine:FindObjectOfEngineType(componentName)
Find GameObject with Unity component.
```lua
local cameraObj = Engine:FindObjectOfEngineType("Camera")
```

#### Engine:FindObjectOfCustomType(fullTypeName)
Find GameObject with custom component.
```lua
local playerObj = Engine:FindObjectOfCustomType("MyGame.PlayerController")
```

### Creating Objects

#### Engine:CreateCube()
Create a cube primitive.
```lua
local cube = Engine:CreateCube()
```

#### Engine:CreateSphere()
Create a sphere primitive.
```lua
local sphere = Engine:CreateSphere()
```

#### Engine:CreateCapsule()
Create a capsule primitive.
```lua
local capsule = Engine:CreateCapsule()
```

#### Engine:CreateCylinder()
Create a cylinder primitive.
```lua
local cylinder = Engine:CreateCylinder()
```

#### Engine:CreatePlane()
Create a plane primitive.
```lua
local plane = Engine:CreatePlane()
```

#### Engine:CreateQuad()
Create a quad primitive.
```lua
local quad = Engine:CreateQuad()
```

#### Engine:CreateEmpty(name)
Create empty GameObject.
```lua
local container = Engine:CreateEmpty("ItemContainer")
```

### Transform Operations

#### Engine:SetPosition(obj, x, y, z)
Set world position.
```lua
Engine:SetPosition(player, 0, 5, 0)
```

#### Engine:SetLocalPosition(obj, x, y, z)
Set local position.
```lua
Engine:SetLocalPosition(childObj, 2, 0, 0)
```

#### Engine:GetPositionX(obj), Engine:GetPositionY(obj), Engine:GetPositionZ(obj)
Get position components.
```lua
local x = Engine:GetPositionX(player)
```

#### Engine:SetEulerAngles(obj, x, y, z)
Set rotation using Euler angles.
```lua
Engine:SetEulerAngles(obj, 0, 90, 0)
```

#### Engine:SetRotation(obj, x, y, z, w)
Set rotation using quaternion.
```lua
Engine:SetRotation(obj, 0, 0, 0, 1)
```

#### Engine:Rotate(obj, x, y, z)
Rotate by angles.
```lua
Engine:Rotate(obj, 0, 45, 0)
```

#### Engine:SetScale(obj, x, y, z)
Set object scale.
```lua
Engine:SetScale(obj, 2, 2, 2)
```

#### Engine:GetScaleX(obj), Engine:GetScaleY(obj), Engine:GetScaleZ(obj)
Get scale components.
```lua
local scaleX = Engine:GetScaleX(obj)
```

#### Engine:Translate(obj, x, y, z)
Move by relative amount.
```lua
Engine:Translate(obj, 0, 0, 1)
```

#### Engine:LookAt(obj, target)
Make object look at target.
```lua
Engine:LookAt(enemy, player)
```

#### Engine:LookAtPosition(obj, x, y, z)
Make object look at position.
```lua
Engine:LookAtPosition(turret, 10, 0, 5)
```

#### Engine:RotateAround(obj, pivotX, pivotY, pivotZ, axisX, axisY, axisZ, angle)
Rotate around point.
```lua
Engine:RotateAround(satellite, 0, 0, 0, 0, 1, 0, 30)
```

### GameObject Properties

#### Engine:SetName(obj, name)
Set GameObject name.
```lua
Engine:SetName(obj, "PowerUp_1")
```

#### Engine:GetName(obj)
Get GameObject name.
```lua
local name = Engine:GetName(obj)
```

#### Engine:SetActive(obj, active)
Set active state.
```lua
Engine:SetActive(menuPanel, false)
```

#### Engine:IsActive(obj)
Check if active.
```lua
if Engine:IsActive(player) then
```

### Hierarchy

#### Engine:SetParent(child, parent)
Set parent object.
```lua
Engine:SetParent(weapon, player)
```

#### Engine:GetParent(obj)
Get parent object.
```lua
local parent = Engine:GetParent(childObj)
```

#### Engine:GetChildCount(obj)
Get number of children.
```lua
local childCount = Engine:GetChildCount(container)
```

#### Engine:GetChild(obj, index)
Get child by index.
```lua
local firstChild = Engine:GetChild(container, 0)
```

### Components

#### Engine:AddEngineComponent(obj, componentName)
Add Unity component.
```lua
Engine:AddEngineComponent(obj, "Rigidbody")
```

#### Engine:AddCustomComponent(obj, fullTypeName)
Add custom component.
```lua
Engine:AddCustomComponent(obj, "MyGame.PlayerController")
```

#### Engine:GetEngineComponent(obj, componentName)
Get Unity component.
```lua
local rigidbody = Engine:GetEngineComponent(player, "Rigidbody")
```

#### Engine:GetCustomComponent(obj, fullTypeName)
Get custom component.
```lua
local script = Engine:GetCustomComponent(player, "MyGame.PlayerController")
```

#### Engine:HasEngineComponent(obj, componentName)
Check for Unity component.
```lua
if Engine:HasEngineComponent(obj, "Collider") then
```

#### Engine:HasCustomComponent(obj, fullTypeName)
Check for custom component.
```lua
if Engine:HasCustomComponent(obj, "MyGame.Health") then
```

#### Engine:SetComponentValue(component, fieldName, value)
Set any component field.
```lua
Engine:SetComponentValue(playerScript, "speed", 10.5)
```

#### Engine:SetComponentFloat(component, fieldName, value)
Set float component field.
```lua
Engine:SetComponentFloat(locomotion, "maxJumpSpeed", 8.5)
```

### Utility

#### Engine:Distance(obj1, obj2)
Distance between objects.
```lua
local dist = Engine:Distance(player, enemy)
```

#### Engine:DistanceToPosition(obj, x, y, z)
Distance to position.
```lua
local dist = Engine:DistanceToPosition(player, 0, 0, 0)
```

#### Engine:DestroyObject(obj)
Destroy GameObject.
```lua
Engine:DestroyObject(bullet)
```

#### Engine:GetKey(key), Engine:GetKeyDown(key), Engine:GetKeyUp(key)
Check keyboard input.
```lua
if Engine:GetKeyDown("space") then
```

#### Engine:GetMouseButton(button), Engine:GetMouseButtonDown(button), Engine:GetMouseButtonUp(button)
Check mouse input.
```lua
if Engine:GetMouseButtonDown(0) then
```

---

## ETime (Time Functions)

### ETime.DeltaTime
Time since last frame.
```lua
local movement = speed * ETime.DeltaTime
```

### ETime.Time
Time since game start.
```lua
local currentTime = ETime.Time
```

### ETime.FixedDeltaTime
Fixed physics timestep.
```lua
local fixedDelta = ETime.FixedDeltaTime
```

---

## EGUI (User Interface)

### Basic Elements

#### EGUI:Label(x, y, width, height, text)
Display text.
```lua
EGUI:Label(10, 10, 200, 30, "Health: " .. health)
```

#### EGUI:Button(x, y, width, height, text)
Clickable button.
```lua
if EGUI:Button(10, 50, 100, 30, "Start") then
```

#### EGUI:TextField(x, y, width, height, text)
Text input field.
```lua
playerName = EGUI:TextField(10, 50, 200, 30, playerName)
```

#### EGUI:TextArea(x, y, width, height, text)
Multi-line text input.
```lua
description = EGUI:TextArea(10, 50, 300, 100, description)
```

#### EGUI:Toggle(x, y, width, height, value, text)
Checkbox.
```lua
showDebug = EGUI:Toggle(10, 10, 150, 30, showDebug, "Debug")
```

#### EGUI:HorizontalSlider(x, y, width, height, value, leftValue, rightValue)
Horizontal slider.
```lua
volume = EGUI:HorizontalSlider(10, 40, 200, 30, volume, 0, 1)
```

#### EGUI:VerticalSlider(x, y, width, height, value, topValue, bottomValue)
Vertical slider.
```lua
brightness = EGUI:VerticalSlider(10, 50, 30, 200, brightness, 1, 0)
```

#### EGUI:Box(x, y, width, height, text)
Container box.
```lua
EGUI:Box(10, 10, 300, 200, "Settings Panel")
```

#### EGUI:Window(id, x, y, width, height, title)
Basic window.
```lua
EGUI:Window(0, 100, 100, 200, 150, "Status")
```

#### EGUI:SelectionGrid(x, y, width, height, selected, texts, xCount)
Grid of options.
```lua
selected = EGUI:SelectionGrid(10, 50, 200, 100, selected, options, 2)
```

#### EGUI:Toolbar(x, y, width, height, selected, texts)
Toolbar.
```lua
selectedTab = EGUI:Toolbar(10, 10, 300, 30, selectedTab, tabs)
```

#### EGUI:HorizontalScrollbar(x, y, width, height, value, size, leftValue, rightValue)
Horizontal scrollbar.
```lua
scrollPos = EGUI:HorizontalScrollbar(10, 200, 200, 20, scrollPos, 0.1, 0, 1)
```

#### EGUI:VerticalScrollbar(x, y, width, height, value, size, topValue, bottomValue)
Vertical scrollbar.
```lua
vScrollPos = EGUI:VerticalScrollbar(300, 50, 20, 200, vScrollPos, 0.1, 0, 1)
```

### Window System

#### EGUI:SetWindowRect(id, x, y, width, height)
Set window bounds.
```lua
EGUI:SetWindowRect(1, 50, 50, 300, 200)
```

#### EGUI:GetWindowX(id), EGUI:GetWindowY(id)
Get window position.
```lua
local winX = EGUI:GetWindowX(1)
```

#### EGUI:DraggableWindow(id, x, y, width, height, title)
Draggable window.
```lua
EGUI:DraggableWindow(1, 100, 100, 250, 200, "Panel")
```

#### EGUI:DragWindow()
Make window draggable.
```lua
EGUI:DragWindow()
```

### Screen Info

#### EGUI:GetScreenWidth(), EGUI:GetScreenHeight()
Screen dimensions.
```lua
local screenW = EGUI:GetScreenWidth()
```

#### EGUI:GetMouseX(), EGUI:GetMouseY()
Mouse position in GUI coords.
```lua
local mouseX = EGUI:GetMouseX()
```

### Colors

#### EGUI:SetColor(r, g, b, a)
Set tint color.
```lua
EGUI:SetColor(1, 0, 0, 1)
```

#### EGUI:SetBackgroundColor(r, g, b, a)
Set background color.
```lua
EGUI:SetBackgroundColor(0, 1, 0, 0.5)
```

#### EGUI:SetContentColor(r, g, b, a)
Set text color.
```lua
EGUI:SetContentColor(0, 0, 1, 1)
```

#### EGUI:ResetColor(), EGUI:ResetBackgroundColor(), EGUI:ResetContentColor()
Reset colors.
```lua
EGUI:ResetColor()
```

---

## EInput (Input Handling)

### Keyboard

#### EInput:GetKey(key), EInput:GetKeyDown(key), EInput:GetKeyUp(key)
Check keyboard input.
```lua
if EInput:GetKeyDown("space") then
```

#### EInput:GetKeyCode(keyCode), EInput:GetKeyCodeDown(keyCode), EInput:GetKeyCodeUp(keyCode)
Check by KeyCode number.
```lua
if EInput:GetKeyCodeDown(32) then
```

### Mouse

#### EInput:GetMouseButton(button), EInput:GetMouseButtonDown(button), EInput:GetMouseButtonUp(button)
Check mouse buttons.
```lua
if EInput:GetMouseButtonDown(0) then
```

#### EInput:GetMouseX(), EInput:GetMouseY()
Mouse position.
```lua
local mouseX = EInput:GetMouseX()
```

#### EInput:GetMouseScrollDelta()
Mouse scroll wheel.
```lua
local scroll = EInput:GetMouseScrollDelta()
```

### Axes

#### EInput:GetAxis(axisName), EInput:GetAxisRaw(axisName)
Get axis input.
```lua
local horizontal = EInput:GetAxis("Horizontal")
```

### Buttons

#### EInput:GetButton(buttonName), EInput:GetButtonDown(buttonName), EInput:GetButtonUp(buttonName)
Check input buttons.
```lua
if EInput:GetButtonDown("Jump") then
```

### Touch

#### EInput:GetTouchCount()
Number of touches.
```lua
local touchCount = EInput:GetTouchCount()
```

#### EInput:GetTouchX(index), EInput:GetTouchY(index)
Touch position.
```lua
local touchX = EInput:GetTouchX(0)
```

#### EInput:GetTouchPhase(index)
Touch phase.
```lua
local phase = EInput:GetTouchPhase(0)
```

### Modifiers

#### EInput:IsShiftHeld(), EInput:IsCtrlHeld(), EInput:IsAltHeld()
Check modifier keys.
```lua
if EInput:IsShiftHeld() then
```

### Utility

#### EInput:AnyKey(), EInput:AnyKeyDown()
Check any key.
```lua
if EInput:AnyKeyDown() then
```

#### EInput:GetInputString()
String input.
```lua
local input = EInput:GetInputString()
```

#### EInput:IsDeviceConnected(deviceName)
Check controller.
```lua
if EInput:IsDeviceConnected("Xbox Controller") then
```

#### EInput:GetJoystickNames()
Get controller names.
```lua
local joysticks = EInput:GetJoystickNames()
```

### Movement Helpers

#### EInput:GetHorizontal(), EInput:GetVertical()
Movement input.
```lua
local h = EInput:GetHorizontal()
```

#### EInput:GetHorizontalRaw(), EInput:GetVerticalRaw()
Raw movement input.
```lua
local hRaw = EInput:GetHorizontalRaw()
```

### Common Inputs

#### EInput:IsJumping(), EInput:IsFiring(), EInput:IsSecondaryFiring(), EInput:IsReloading()
Common game inputs.
```lua
if EInput:IsJumping() then
```

#### EInput:IsEscapePressed(), EInput:IsEnterPressed(), EInput:IsSpacePressed()
Common key checks.
```lua
if EInput:IsEscapePressed() then
```

#### EInput:IsWPressed(), EInput:IsAPressed(), EInput:IsSPressed(), EInput:IsDPressed()
WASD keys.
```lua
if EInput:IsWPressed() then
```

#### EInput:IsUpArrow(), EInput:IsDownArrow(), EInput:IsLeftArrow(), EInput:IsRightArrow()
Arrow keys.
```lua
if EInput:IsUpArrow() then
```

### VR Input (Hand: 0=Left, 1=Right)

#### EInput:GetVRGripButtonDown(hand)
VR grip button.
```lua
if EInput:GetVRGripButtonDown(1) then
```

#### EInput:GetVRTriggerButtonDown(hand)
VR trigger button.
```lua
if EInput:GetVRTriggerButtonDown(1) then
```

#### EInput:GetVRTriggerButtonTouched(hand)
VR trigger touch.
```lua
if EInput:GetVRTriggerButtonTouched(1) then
```

#### EInput:GetVRGripButtonFloat(hand)
VR grip pressure.
```lua
local grip = EInput:GetVRGripButtonFloat(1)
```

#### EInput:GetVRTriggerButtonFloat(hand)
VR trigger pressure.
```lua
local trigger = EInput:GetVRTriggerButtonFloat(1)
```

#### EInput:GetVRPrimaryButtonDown(hand)
VR primary button (A/X).
```lua
if EInput:GetVRPrimaryButtonDown(1) then
```

#### EInput:GetVRPrimaryButtonTouched(hand)
VR primary button touch.
```lua
if EInput:GetVRPrimaryButtonTouched(1) then
```

#### EInput:GetVRSecondaryButtonDown(hand)
VR secondary button (B/Y).
```lua
if EInput:GetVRSecondaryButtonDown(1) then
```

#### EInput:GetVRSecondaryButtonTouched(hand)
VR secondary button touch.
```lua
if EInput:GetVRSecondaryButtonTouched(1) then
```

#### EInput:GetVRThumbStickButtonDown(hand)
VR thumbstick click.
```lua
if EInput:GetVRThumbStickButtonDown(1) then
```

#### EInput:GetVRThumbStickButtonTouched(hand)
VR thumbstick touch.
```lua
if EInput:GetVRThumbStickButtonTouched(1) then
```

#### EInput:GetVRThumbStickX(hand), EInput:GetVRThumbStickY(hand)
VR thumbstick axes.
```lua
local stickX = EInput:GetVRThumbStickX(1)
```

#### EInput:GetVRDeviceVelocityX(hand), EInput:GetVRDeviceVelocityY(hand), EInput:GetVRDeviceVelocityZ(hand)
VR controller velocity.
```lua
local velX = EInput:GetVRDeviceVelocityX(1)
```

---

## EPhysics (Physics Operations)

### Forces

#### EPhysics:AddForce(obj, x, y, z)
Add force to rigidbody.
```lua
EPhysics:AddForce(player, 0, 10, 0)
```

#### EPhysics:AddForceAtPosition(obj, forceX, forceY, forceZ, posX, posY, posZ)
Add force at position.
```lua
EPhysics:AddForceAtPosition(obj, 100, 0, 0, 5, 0, 0)
```

#### EPhysics:AddTorque(obj, x, y, z)
Add rotational force.
```lua
EPhysics:AddTorque(obj, 0, 100, 0)
```

### Velocity

#### EPhysics:SetVelocity(obj, x, y, z)
Set velocity directly.
```lua
EPhysics:SetVelocity(projectile, 0, 0, 20)
```

#### EPhysics:GetVelocityX(obj), EPhysics:GetVelocityY(obj), EPhysics:GetVelocityZ(obj)
Get velocity components.
```lua
local velY = EPhysics:GetVelocityY(player)
```

#### EPhysics:SetAngularVelocity(obj, x, y, z)
Set rotational velocity.
```lua
EPhysics:SetAngularVelocity(obj, 0, 5, 0)
```

### Properties

#### EPhysics:SetMass(obj, mass)
Set object mass.
```lua
EPhysics:SetMass(obj, 100)
```

#### EPhysics:GetMass(obj)
Get object mass.
```lua
local mass = EPhysics:GetMass(player)
```

#### EPhysics:SetUseGravity(obj, useGravity)
Enable/disable gravity.
```lua
EPhysics:SetUseGravity(obj, false)
```

#### EPhysics:SetKinematic(obj, isKinematic)
Set kinematic state.
```lua
EPhysics:SetKinematic(obj, true)
```

#### EPhysics:SetDrag(obj, drag)
Set air resistance.
```lua
EPhysics:SetDrag(obj, 10)
```

#### EPhysics:SetAngularDrag(obj, angularDrag)
Set rotational resistance.
```lua
EPhysics:SetAngularDrag(obj, 20)
```

### Raycasting

#### EPhysics:Raycast(x, y, z, dirX, dirY, dirZ, distance)
Check raycast hit.
```lua
local hit = EPhysics:Raycast(0, 5, 0, 0, -1, 0, 10)
```

#### EPhysics:RaycastHit(x, y, z, dirX, dirY, dirZ, distance)
Get hit object.
```lua
local hitObj = EPhysics:RaycastHit(0, 5, 0, 0, -1, 0, 10)
```

### Gravity

#### EPhysics:SetGravity(x, y, z)
Set global gravity.
```lua
EPhysics:SetGravity(0, -20, 0)
```

#### EPhysics:GetGravityX(), EPhysics:GetGravityY(), EPhysics:GetGravityZ()
Get gravity components.
```lua
local gravityY = EPhysics:GetGravityY()
```

### Constraints

#### EPhysics:FreezePosition(obj, x, y, z)
Freeze position axes.
```lua
EPhysics:FreezePosition(obj, true, false, true)
```

#### EPhysics:FreezeRotation(obj, x, y, z)
Freeze rotation axes.
```lua
EPhysics:FreezeRotation(obj, true, false, true)
```

#### EPhysics:HasRigidbody(obj)
Check for rigidbody.
```lua
if EPhysics:HasRigidbody(obj) then
```

---

## EAudio (Audio Control)

### Playback

#### EAudio:Play(obj), EAudio:Stop(obj), EAudio:Pause(obj), EAudio:UnPause(obj)
Control audio playback.
```lua
EAudio:Play(musicPlayer)
```

#### EAudio:IsPlaying(obj)
Check if playing.
```lua
if EAudio:IsPlaying(musicPlayer) then
```

### Volume

#### EAudio:SetVolume(obj, volume), EAudio:GetVolume(obj)
Control volume.
```lua
EAudio:SetVolume(musicPlayer, 0.5)
```

### Pitch

#### EAudio:SetPitch(obj, pitch), EAudio:GetPitch(obj)
Control pitch.
```lua
EAudio:SetPitch(sfxPlayer, 1.5)
```

### Looping

#### EAudio:SetLoop(obj, loop), EAudio:IsLooping(obj)
Control looping.
```lua
EAudio:SetLoop(musicPlayer, true)
```

### Time

#### EAudio:SetTime(obj, time), EAudio:GetTime(obj)
Control playback position.
```lua
EAudio:SetTime(musicPlayer, 30)
```

#### EAudio:GetClipLength(obj)
Get audio length.
```lua
local length = EAudio:GetClipLength(musicPlayer)
```

### 3D Audio

#### EAudio:SetSpatialBlend(obj, spatialBlend)
Set 3D blend.
```lua
EAudio:SetSpatialBlend(audioObject, 1.0)
```

#### EAudio:SetMinDistance(obj, minDistance), EAudio:SetMaxDistance(obj, maxDistance)
Set 3D distances.
```lua
EAudio:SetMinDistance(footstepAudio, 1.0)
```

### Utility

#### EAudio:SetMute(obj, mute), EAudio:IsMuted(obj)
Mute control.
```lua
EAudio:SetMute(audioObject, true)
```

#### EAudio:SetPlayOnAwake(obj, playOnAwake)
Auto-play setting.
```lua
EAudio:SetPlayOnAwake(audioObject, false)
```

#### EAudio:HasAudioSource(obj)
Check for AudioSource.
```lua
if EAudio:HasAudioSource(obj) then
```

### Global Audio

#### EAudio:SetGlobalVolume(volume), EAudio:GetGlobalVolume()
Master volume.
```lua
EAudio:SetGlobalVolume(0.8)
```

#### EAudio:SetGlobalPause(pause), EAudio:IsGlobalPaused()
Global pause.
```lua
EAudio:SetGlobalPause(true)
```

#### EAudio:PlayClipAtPoint(clipName, x, y, z, volume)
Play sound at position.
```lua
EAudio:PlayClipAtPoint("ExplosionSound", 0, 0, 0, 1.0)
```

---

## EScene (Scene Management)

### Loading

#### EScene:LoadScene(sceneName), EScene:LoadSceneAsync(sceneName)
Load scenes.
```lua
EScene:LoadScene("MainMenu")
```

#### EScene:LoadSceneByIndex(sceneIndex)
Load by index.
```lua
EScene:LoadSceneByIndex(1)
```

#### EScene:LoadSceneAdditive(sceneName), EScene:UnloadScene(sceneName)
Additive loading.
```lua
EScene:LoadSceneAdditive("UIScene")
```

#### EScene:ReloadScene(), EScene:LoadNextScene(), EScene:LoadPreviousScene()
Scene navigation.
```lua
EScene:ReloadScene()
```

### Information

#### EScene:GetActiveSceneName(), EScene:GetActiveSceneIndex()
Get scene info.
```lua
local sceneName = EScene:GetActiveSceneName()
```

#### EScene:GetSceneCount(), EScene:GetSceneCountInBuildSettings()
Get scene counts.
```lua
local sceneCount = EScene:GetSceneCount()
```

### Time Control

#### EScene:SetTimeScale(timeScale), EScene:GetTimeScale()
Control time speed.
```lua
EScene:SetTimeScale(0.5)
```

#### EScene:PauseGame(), EScene:ResumeGame(), EScene:IsGamePaused()
Pause control.
```lua
EScene:PauseGame()
```

### Application

#### EScene:QuitGame()
Quit application.
```lua
EScene:QuitGame()
```

#### EScene:SetTargetFrameRate(frameRate), EScene:GetTargetFrameRate()
Frame rate control.
```lua
EScene:SetTargetFrameRate(60)
```

#### EScene:SetVSyncCount(vSyncCount), EScene:GetVSyncCount()
VSync control.
```lua
EScene:SetVSyncCount(1)
```

#### EScene:GetApplicationVersion(), EScene:GetPlatform()
Get app info.
```lua
local version = EScene:GetApplicationVersion()
```

#### EScene:IsFocused(), EScene:IsPlaying()
Check app state.
```lua
if EScene:IsFocused() then
```

#### EScene:OpenURL(url)
Open web URL.
```lua
EScene:OpenURL("https://example.com")
```

#### EScene:SetRunInBackground(runInBackground), EScene:GetRunInBackground()
Background running.
```lua
EScene:SetRunInBackground(true)
```

### Paths

#### EScene:GetDataPath(), EScene:GetPersistentDataPath(), EScene:GetStreamingAssetsPath(), EScene:GetTemporaryCachePath()
Get file paths.
```lua
local dataPath = EScene:GetDataPath()
```

#### EScene:DontDestroyOnLoad(obj)
Persist object across scenes.
```lua
EScene:DontDestroyOnLoad(musicPlayer)
```

---

## EMath (Math Utilities)

### Basic Math

#### EMath:Abs(value), EMath:Sqrt(value), EMath:Pow(value, power)
Basic operations.
```lua
local abs = EMath:Abs(-5)
```

#### EMath:Sin(radians), EMath:Cos(radians), EMath:Tan(radians)
Trigonometry.
```lua
local sin = EMath:Sin(EMath:PI() / 2)
```

#### EMath:Asin(value), EMath:Acos(value), EMath:Atan(value), EMath:Atan2(y, x)
Inverse trig.
```lua
local angle = EMath:Atan2(y, x)
```

#### EMath:DegToRad(degrees), EMath:RadToDeg(radians)
Angle conversion.
```lua
local radians = EMath:DegToRad(90)
```

### Min/Max/Clamp

#### EMath:Min(a, b), EMath:Max(a, b)
Min/max values.
```lua
local smaller = EMath:Min(5, 10)
```

#### EMath:Clamp(value, min, max), EMath:Clamp01(value)
Clamp values.
```lua
local clamped = EMath:Clamp(15, 0, 10)
```

### Interpolation

#### EMath:Lerp(a, b, t), EMath:LerpUnclamped(a, b, t)
Linear interpolation.
```lua
local lerped = EMath:Lerp(0, 10, 0.5)
```

#### EMath:InverseLerp(a, b, value)
Inverse interpolation.
```lua
local t = EMath:InverseLerp(0, 10, 5)
```

#### EMath:SmoothStep(from, to, t)
Smooth interpolation.
```lua
local smooth = EMath:SmoothStep(0, 10, 0.5)
```

#### EMath:MoveTowards(current, target, maxDelta)
Move towards target.
```lua
local moved = EMath:MoveTowards(5, 10, 2)
```

### Wave Functions

#### EMath:PingPong(t, length)
Ping pong between 0 and length.
```lua
local ping = EMath:PingPong(time, 5)
```

#### EMath:Repeat(t, length)
Repeat between 0 and length.
```lua
local repeated = EMath:Repeat(time, 10)
```

### Rounding

#### EMath:Round(value), EMath:RoundToInt(value)
Round values.
```lua
local rounded = EMath:Round(3.7)
```

#### EMath:Floor(value), EMath:FloorToInt(value)
Floor values.
```lua
local floored = EMath:Floor(3.7)
```

#### EMath:Ceil(value), EMath:CeilToInt(value)
Ceiling values.
```lua
local ceiled = EMath:Ceil(3.2)
```

#### EMath:Sign(value)
Get sign of value.
```lua
local sign = EMath:Sign(-5)
```

### Logarithms

#### EMath:Log(value), EMath:Log10(value), EMath:Exp(value)
Logarithmic functions.
```lua
local log = EMath:Log(10)
```

### Vector Math

#### EMath:Distance(x1, y1, x2, y2), EMath:Distance3D(x1, y1, z1, x2, y2, z2)
Distance calculations.
```lua
local dist = EMath:Distance3D(0, 0, 0, 1, 1, 1)
```

#### EMath:Magnitude(x, y), EMath:Magnitude3D(x, y, z)
Vector magnitude.
```lua
local mag = EMath:Magnitude3D(1, 1, 1)
```

#### EMath:Dot(x1, y1, x2, y2), EMath:Dot3D(x1, y1, z1, x2, y2, z2)
Dot product.
```lua
local dot = EMath:Dot3D(1, 0, 0, 0, 1, 0)
```

#### EMath:Angle(x1, y1, x2, y2), EMath:Angle3D(x1, y1, z1, x2, y2, z2)
Angle between vectors.
```lua
local angle = EMath:Angle3D(1, 0, 0, 0, 1, 0)
```

### Angle Math

#### EMath:LerpAngle(a, b, t)
Interpolate angles.
```lua
local angle = EMath:LerpAngle(0, 360, 0.5)
```

#### EMath:DeltaAngle(current, target)
Shortest angle difference.
```lua
local delta = EMath:DeltaAngle(350, 10)
```

### Constants

#### EMath:PI(), EMath:Infinity(), EMath:NegativeInfinity(), EMath:Epsilon()
Math constants.
```lua
local pi = EMath:PI()
```

---

## EUtility (General Utilities)

### Random

#### EUtility:RandomRange(min, max), EUtility:RandomRangeInt(min, max)
Random numbers.
```lua
local randomFloat = EUtility:RandomRange(1.0, 10.0)
```

#### EUtility:RandomValue()
Random 0-1.
```lua
local random = EUtility:RandomValue()
```

#### EUtility:SetRandomSeed(seed)
Set random seed.
```lua
EUtility:SetRandomSeed(12345)
```

#### EUtility:RandomBool(), EUtility:RandomNormal()
Random utilities.
```lua
local randomBool = EUtility:RandomBool()
```

### Cursor

#### EUtility:SetCursorVisible(visible), EUtility:IsCursorVisible()
Cursor visibility.
```lua
EUtility:SetCursorVisible(false)
```

#### EUtility:SetCursorLocked(locked), EUtility:IsCursorLocked()
Cursor locking.
```lua
EUtility:SetCursorLocked(true)
```

#### EUtility:SetCursorConfinedToWindow(confined)
Confine cursor to window.
```lua
EUtility:SetCursorConfinedToWindow(true)
```

### Debug Output

#### EUtility:Print(message), EUtility:PrintWarning(message), EUtility:PrintError(message)
Debug printing.
```lua
EUtility:Print("Debug message")
```

### Debug Drawing

#### EUtility:DrawLine(x1, y1, z1, x2, y2, z2, duration)
Draw debug line.
```lua
EUtility:DrawLine(0, 0, 0, 10, 0, 0, 2.0)
```

#### EUtility:DrawLineColored(x1, y1, z1, x2, y2, z2, r, g, b, duration)
Draw colored line.
```lua
EUtility:DrawLineColored(0, 0, 0, 0, 10, 0, 1, 0, 0, 5.0)
```

#### EUtility:DrawRay(x, y, z, dirX, dirY, dirZ, duration)
Draw debug ray.
```lua
EUtility:DrawRay(0, 0, 0, 1, 0, 0, 2.0)
```

#### EUtility:DrawRayColored(x, y, z, dirX, dirY, dirZ, r, g, b, duration)
Draw colored ray.
```lua
EUtility:DrawRayColored(0, 0, 0, 1, 0, 0, 0, 1, 0, 2.0)
```

#### EUtility:DrawLineBetweenObjects(obj1, obj2, duration)
Draw line between objects.
```lua
EUtility:DrawLineBetweenObjects(player, enemy, 1.0)
```

#### EUtility:DrawLineBetweenObjectsColored(obj1, obj2, r, g, b, duration)
Draw colored line between objects.
```lua
EUtility:DrawLineBetweenObjectsColored(obj1, obj2, 1, 0, 0, 2.0)
```

### String Formatting

#### EUtility:FormatFloat(value, decimals)
Format float to string.
```lua
local formatted = EUtility:FormatFloat(3.14159, 2)
```

#### EUtility:FormatTime(seconds), EUtility:FormatTimeWithHours(seconds)
Format time.
```lua
local timeStr = EUtility:FormatTime(125)
```

### String Parsing

#### EUtility:ParseFloat(value), EUtility:ParseInt(value), EUtility:ParseBool(value)
Parse strings.
```lua
local number = EUtility:ParseFloat("3.14")
```

### Clipboard

#### EUtility:CopyToClipboard(text), EUtility:GetFromClipboard()
Clipboard operations.
```lua
EUtility:CopyToClipboard("Hello World")
```

### Screenshots

#### EUtility:TakeScreenshot(filename)
Take screenshot.
```lua
EUtility:TakeScreenshot("screenshot.png")
```

### Screen Info

#### EUtility:GetScreenWidth(), EUtility:GetScreenHeight(), EUtility:GetScreenDPI()
Screen information.
```lua
local width = EUtility:GetScreenWidth()
```

#### EUtility:IsFullscreen(), EUtility:SetFullscreen(fullscreen)
Fullscreen control.
```lua
EUtility:SetFullscreen(true)
```

#### EUtility:SetResolution(width, height, fullscreen)
Set screen resolution.
```lua
EUtility:SetResolution(1920, 1080, true)
```

### Quality Settings

#### EUtility:SetQualityLevel(qualityLevel), EUtility:GetQualityLevel()
Quality control.
```lua
EUtility:SetQualityLevel(2)
```

#### EUtility:GetQualityNames()
Get quality setting names.
```lua
local names = EUtility:GetQualityNames()
```

#### EUtility:SetMasterTextureLimit(limit)
Set texture quality.
```lua
EUtility:SetMasterTextureLimit(0)
```

#### EUtility:SetShadowDistance(distance)
Set shadow distance.
```lua
EUtility:SetShadowDistance(100)
```

### Time Utilities

#### EUtility:GetRealTimeSinceStartup(), EUtility:GetFrameCount()
Time information.
```lua
local realTime = EUtility:GetRealTimeSinceStartup()
```

#### EUtility:SetFixedDeltaTime(fixedDeltaTime), EUtility:SetMaximumDeltaTime(maximumDeltaTime)
Time settings.
```lua
EUtility:SetFixedDeltaTime(0.02)
```

### Value Checking

#### EUtility:IsNaN(value), EUtility:IsInfinity(value)
Check special float values.
```lua
if EUtility:IsNaN(value) then
```

### GameObject Utilities

#### EUtility:SetLayerMask(obj, layer), EUtility:GetLayerMask(obj)
Layer control.
```lua
EUtility:SetLayerMask(obj, 8)
```

#### EUtility:SetTag(obj, tag), EUtility:GetTag(obj)
Tag control.
```lua
EUtility:SetTag(obj, "Player")
```

#### EUtility:CompareTag(obj, tag)
Compare tags.
```lua
if EUtility:CompareTag(obj, "Enemy") then
```

#### EUtility:Instantiate(prefab, x, y, z), EUtility:InstantiateAndReturn(prefab, x, y, z)
Instantiate objects.
```lua
local newObj = EUtility:InstantiateAndReturn(prefab, 0, 0, 0)
```

#### EUtility:Wait(seconds)
Wait (blocking).
```lua
EUtility:Wait(2.0)
```

---

## Lifecycle Functions

Your Lua scripts can implement these functions that get called automatically:

### Start()
Called once when the script loads.
```lua
function Start()
    Debug:Log("Script started!")
    player = Engine:FindGameObject("Player")
end
```

### Update()
Called every frame.
```lua
function Update()
    if EInput:GetKeyDown("f") then
        Debug:Log("F pressed!")
    end
end
```

### FixedUpdate()
Called at fixed intervals for physics.
```lua
function FixedUpdate()
    -- Physics code here
end
```

### LateUpdate()
Called after all Update functions.
```lua
function LateUpdate()
    -- Camera follow code here
end
```

### OnGUI()
Called for GUI rendering.
```lua
function OnGUI()
    EGUI:Label(10, 10, 200, 30, "Hello GUI!")
end
```

### OnDestroy()
Called when script is destroyed.
```lua
function OnDestroy()
    Debug:Log("Script destroyed")
end
```

### OnPause(), OnResume()
Called when application is paused/resumed.
```lua
function OnPause()
    Debug:Log("Game paused")
end
```

### OnUnloaded()
Called when extensions are being unloaded to restart or on application shutdown
```lua
function OnUnloaded
    -- Set any references nil and undo most boolean logic
    Debug:Log("My extension unloaded!")
end
```

### OnFocus(), OnLostFocus()
Called when application gains/loses focus.
```lua
function OnFocus()
    Debug:Log("Game focused")
end
```

---

## Complete Example: Simple Player Controller

```lua
-- SimplePlayer.lua
local player = nil
local speed = 5.0
local jumpForce = 10.0
local health = 100

function Start()
    player = Engine:FindGameObject("Player")
    if not player then
        Debug:LogError("Player not found!")
        return
    end
    
    if not EPhysics:HasRigidbody(player) then
        Engine:AddEngineComponent(player, "Rigidbody")
    end
    
    Debug:Log("Player controller ready!")
end

function Update()
    if not player then return end
    
    -- Movement
    local h = EInput:GetHorizontal()
    local v = EInput:GetVertical()
    
    if h ~= 0 or v ~= 0 then
        Engine:Translate(player, h * speed * ETime.DeltaTime, 0, v * speed * ETime.DeltaTime)
    end
    
    -- Jump
    if EInput:IsJumping() then
        EPhysics:AddForce(player, 0, jumpForce, 0)
    end
    
    -- Debug info
    if EInput:GetKeyDown("i") then
        local x = Engine:GetPositionX(player)
        local y = Engine:GetPositionY(player)
        local z = Engine:GetPositionZ(player)
        Debug:Log("Position: " .. x .. ", " .. y .. ", " .. z)
    end
end

function OnGUI()
    EGUI:Label(10, 10, 200, 30, "Health: " .. health)
    EGUI:Label(10, 50, 300, 30, "WASD: Move, Space: Jump, I: Debug")
end

function OnUnloaded()
    player = nil
    Debug:Log("Player Controller Unloaded!")
end
```

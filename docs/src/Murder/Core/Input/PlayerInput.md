# PlayerInput

**Namespace:** Murder.Core.Input \
**Assembly:** Murder.dll

```csharp
public class PlayerInput
```

The central input manager that tracks button and axis state for keyboard, mouse, and gamepad each frame.

**Intent:** Provide a single, game-accessible object for registering bindings and querying input state.

**Use-case:** Access `Game.Input` (a `PlayerInput` instance) in any system or service. Call `Register()` at startup to bind keys/buttons to logical IDs, then call `Pressed()`, `Down()`, `GetAxis()`, and `VerticalMenu()` each frame to drive gameplay and UI.

### ⭐ Constructors
```csharp
public PlayerInput()
```

### ⭐ Properties
#### AllAxis
```csharp
public Int32[] AllAxis { get; }
```

All registered axis IDs (debug only).

**Returns** \
[int[]](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### AllButtons
```csharp
public Int32[] AllButtons { get; }
```

All registered button IDs (debug only).

**Returns** \
[int[]](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### CursorPosition
```csharp
public Point CursorPosition;
```

Cursor position on the screen. Null when using an ImGui window.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \
#### KeyboardConsumed
```csharp
public bool KeyboardConsumed;
```

Keyboard ignored because the player is probably typing something on ImGui

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### MouseConsumed
```csharp
public bool MouseConsumed;
```

When `true`, mouse input is suppressed for this frame (e.g., the ImGui window has focus).

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### ScrollWheel
```csharp
public int ScrollWheel { get; }
```

Scrollwheel delta

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### UsingKeyboard
```csharp
public bool UsingKeyboard;
```

If true player is using the keyboard, false means the player is using a game controller

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
### ⭐ Methods
#### Down(Keys)
```csharp
public bool Down(Keys key)
```

Returns `true` if `key` is currently held.

**Parameters** \
`key` [Keys](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Keys.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Down(int, bool)
```csharp
public bool Down(int button, bool raw)
```

Returns `true` if the virtual button `button` is currently held. When `raw` is `true`, ignores the consumed flag.

**Parameters** \
`button` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`raw` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### GridMenu(GenericMenuInfo`1&, int, int, GridMenuFlags)
```csharp
public bool GridMenu(GenericMenuInfo`1& currentInfo, int width, int size, GridMenuFlags gridMenuFlags)
```

Advances a typed grid menu by one frame and returns `true` if the submit button was pressed.

**Parameters** \
`currentInfo` [GenericMenuInfo\<T\>&](../../../Murder/Core/Input/GenericMenuInfo-1.html) \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`size` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`gridMenuFlags` [GridMenuFlags](../../../Murder/Core/Input/GridMenuFlags.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### GridMenu(MenuInfo&, int, int, int, GridMenuFlags)
```csharp
public bool GridMenu(MenuInfo& currentInfo, int width, int _, int size, GridMenuFlags gridMenuFlags)
```

Advances a `MenuInfo` grid menu by one frame and returns `true` if the submit button was pressed.

**Parameters** \
`currentInfo` [MenuInfo&](../../../Murder/Core/Input/MenuInfo.html) \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`_` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`size` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`gridMenuFlags` [GridMenuFlags](../../../Murder/Core/Input/GridMenuFlags.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HorizontalMenu(MenuInfo&)
```csharp
public bool HorizontalMenu(MenuInfo& currentInfo)
```

Advances a horizontal `MenuInfo` by one frame and returns `true` if the submit button was pressed.

**Parameters** \
`currentInfo` [MenuInfo&](../../../Murder/Core/Input/MenuInfo.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HorizontalMenu(Int32&, int)
```csharp
public bool HorizontalMenu(Int32& selectedOption, int length)
```

Navigates a simple horizontal list of `length` items and returns `true` if submit was pressed.

**Parameters** \
`selectedOption` [int&](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`length` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Pressed(Keys)
```csharp
public bool Pressed(Keys enter)
```

Returns `true` if `enter` was just pressed this frame.

**Parameters** \
`enter` [Keys](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Keys.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Pressed(int, bool)
```csharp
public bool Pressed(int button, bool raw)
```

Returns `true` if the virtual button `button` was just pressed this frame. When `raw` is `true`, ignores the consumed flag.

**Parameters** \
`button` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`raw` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### PressedAndConsume(int)
```csharp
public bool PressedAndConsume(int button)
```

Returns `true` if `button` was just pressed, and immediately consumes it so subsequent reads return `false`.

**Parameters** \
`button` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Released(int)
```csharp
public bool Released(int button)
```

Returns `true` if `button` was released this frame.

**Parameters** \
`button` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Shortcut(Keys, Keys[])
```csharp
public bool Shortcut(Keys key, Keys[] modifiers)
```

Returns `true` if `key` was just pressed while all `modifiers` are held.

**Parameters** \
`key` [Keys](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Keys.html) \
`modifiers` [Keys[]](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Keys.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Shortcut(Chord)
```csharp
public bool Shortcut(Chord chord)
```

Returns `true` if `chord` (key + modifiers) was just activated this frame.

**Parameters** \
`chord` [Chord](../../../Murder/Core/Input/Chord.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### SimpleVerticalMenu(Int32&, int)
```csharp
public bool SimpleVerticalMenu(Int32& selectedOption, int length)
```

Navigates a simple vertical list of `length` items and returns `true` if submit was pressed.

**Parameters** \
`selectedOption` [int&](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`length` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### VerticalMenu(GenericMenuInfo`1&)
```csharp
public bool VerticalMenu(GenericMenuInfo`1& currentInfo)
```

Advances a typed vertical menu by one frame and returns `true` if the submit button was pressed.

**Parameters** \
`currentInfo` [GenericMenuInfo\<T\>&](../../../Murder/Core/Input/GenericMenuInfo-1.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### VerticalMenu(MenuInfo&)
```csharp
public bool VerticalMenu(MenuInfo& currentInfo)
```

Advances a vertical `MenuInfo` by one frame and returns `true` if the submit button was pressed.

**Parameters** \
`currentInfo` [MenuInfo&](../../../Murder/Core/Input/MenuInfo.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### GetAxisDescriptor(int)
```csharp
public string GetAxisDescriptor(int axis)
```

Returns a human-readable description of the bindings registered for axis `axis`.

**Parameters** \
`axis` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### GetButtonDescriptor(int)
```csharp
public string GetButtonDescriptor(int button)
```

Returns a human-readable description of the bindings registered for button `button`.

**Parameters** \
`button` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### GetKeyboardInput()
```csharp
public string GetKeyboardInput()
```

Returns the accumulated typed text from keyboard input since the last frame.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### GetAxis(int)
```csharp
public VirtualAxis GetAxis(int axis)
```

Returns the `VirtualAxis` registered under `axis`. Throws if not found.

**Parameters** \
`axis` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[VirtualAxis](../../../Murder/Core/Input/VirtualAxis.html) \

#### GetOrCreateAxis(int)
```csharp
public VirtualAxis GetOrCreateAxis(int axis)
```

Returns an existing `VirtualAxis` for `axis`, or creates and registers a new one.

**Parameters** \
`axis` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[VirtualAxis](../../../Murder/Core/Input/VirtualAxis.html) \

#### GetOrCreateButton(int)
```csharp
public VirtualButton GetOrCreateButton(int button)
```

Returns an existing `VirtualButton` for `button`, or creates and registers a new one.

**Parameters** \
`button` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[VirtualButton](../../../Murder/Core/Input/VirtualButton.html) \

#### Bind(int, Action<T>)
```csharp
public void Bind(int button, Action<T> action)
```

Registers `action` to be called every time `button` is pressed.

**Parameters** \
`button` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`action` [Action\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Action-1?view=net-7.0) \

#### ClampText(int)
```csharp
public void ClampText(int size)
```

Truncates the current keyboard text buffer to `size` characters.

**Parameters** \
`size` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### ClearBinds(int)
```csharp
public void ClearBinds(int button)
```

Clears all binds from a button

**Parameters** \
`button` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Consume(int)
```csharp
public void Consume(int button)
```

Consumes all buttons that have anything in common with this

**Parameters** \
`button` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
\

#### ConsumeAll()
```csharp
public void ConsumeAll()
```

Marks all registered buttons and axes as consumed for the current frame.

#### ListenToKeyboardInput(bool, int)
```csharp
public void ListenToKeyboardInput(bool enable, int maxCharacters)
```

Enables or disables raw keyboard text capture, limiting input to `maxCharacters`.

**Parameters** \
`enable` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`maxCharacters` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Register(int, InputButtonAxis[])
```csharp
public void Register(int axis, InputButtonAxis[] buttonAxes)
```

Registers input axes

**Parameters** \
`axis` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`buttonAxes` [InputButtonAxis[]](../../../Murder/Core/Input/InputButtonAxis.html) \

#### Register(int, Buttons[])
```csharp
public void Register(int button, Buttons[] buttons)
```

Registers a mouse button as a button

**Parameters** \
`button` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`buttons` [Buttons[]](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Buttons.html) \

#### Register(int, Keys[])
```csharp
public void Register(int button, Keys[] keys)
```

Registers a keyboard key as a button

**Parameters** \
`button` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`keys` [Keys[]](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Keys.html) \

#### Register(int, MouseButtons[])
```csharp
public void Register(int button, MouseButtons[] buttons)
```

Registers mouse buttons as bindings for virtual button `button`.

**Parameters** \
`button` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`buttons` [MouseButtons[]](../../../Murder/Core/Input/MouseButtons.html) \

#### RegisterAxes(int, GamepadAxis[])
```csharp
public void RegisterAxes(int axis, GamepadAxis[] gamepadAxis)
```

Registers a gamepad axis as a button

**Parameters** \
`axis` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`gamepadAxis` [GamepadAxis[]](../../../Murder/Core/Input/GamepadAxis.html) \

#### RegisterAxesAsButton(int, GamepadAxis[])
```csharp
public void RegisterAxesAsButton(int button, GamepadAxis[] gamepadAxis)
```

Registers a gamepad axis as a button

**Parameters** \
`button` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`gamepadAxis` [GamepadAxis[]](../../../Murder/Core/Input/GamepadAxis.html) \

#### Update()
```csharp
public void Update()
```

Pulls new device state each frame and updates all registered buttons and axes.



⚡
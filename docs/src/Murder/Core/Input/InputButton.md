# InputButton

**Namespace:** Murder.Core.Input \
**Assembly:** Murder.dll

```csharp
public sealed struct InputButton : IEquatable<T>
```

Represents a single physical control — a keyboard key, a gamepad button, a mouse button, or a gamepad analog axis — bound to one logical input slot.

**Intent:** This is the smallest building block of Murder's input system: a `VirtualButton` is a list of `InputButton` alternatives (any of which triggers it), and an `InputButtonAxis` combines four of them (or a single analog one) into a 2D direction.

**Use-case:** Game code rarely constructs an `InputButton` directly outside of `PlayerInput.Register()` calls or editor rebinding UI; most gameplay code instead queries `PlayerInput` by logical id (e.g. `Pressed(int)`, `Down(int)`) rather than working with `InputButton` values.

**Implements:** _[IEquatable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.IEquatable-1?view=net-7.0)_

### ⭐ Constructors

```csharp
public InputButton()
```

Creates an empty, unbound button (`Source` is `InputSource.None`). Used as a placeholder before a real binding is assigned.

```csharp
public InputButton(Buttons button)
```

Binds this input to a digital gamepad button.

**Parameters** \
`button` [Buttons](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Buttons.html) \
The gamepad button that triggers this binding. \

```csharp
public InputButton(Keys key)
```

Binds this input to a keyboard key.

**Parameters** \
`key` [Keys](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Keys.html) \
The keyboard key that triggers this binding. \

```csharp
public InputButton(GamepadAxis axis)
```

Binds this input to a gamepad analog axis (thumbstick or D-pad treated as an axis) rather than a discrete button.

**Parameters** \
`axis` [GamepadAxis](../../../Murder/Core/Input/GamepadAxis.html) \
The gamepad axis that this binding reads. \

```csharp
public InputButton(MouseButtons button)
```

Binds this input to a mouse button.

**Parameters** \
`button` [MouseButtons](../../../Murder/Core/Input/MouseButtons.html) \
The mouse button that triggers this binding. \

```csharp
public InputButton(InputSource source, Nullable<Keys> keys, Nullable<Buttons> buttons, Nullable<MouseButtons> mouseButtons, Nullable<GamepadAxis> gamepadAxis)
```

Low-level constructor that sets every backing field directly, used when deserializing a saved binding (e.g. from `ButtonBindingsInfo` or `AxisBindingsInfo`) whose `InputSource` is already known.

**Parameters** \
`source` [InputSource](../../../Murder/Core/Input/InputSource.html) \
The device family this binding reads from. \
`keys` [Keys?](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Keys.html) \
The keyboard key, when `source` is `InputSource.Keyboard`. \
`buttons` [Buttons?](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Buttons.html) \
The gamepad button, when `source` is `InputSource.Gamepad`. \
`mouseButtons` [MouseButtons?](../../../Murder/Core/Input/MouseButtons.html) \
The mouse button, when `source` is `InputSource.Mouse`. \
`gamepadAxis` [GamepadAxis?](../../../Murder/Core/Input/GamepadAxis.html) \
The gamepad axis, when `source` is `InputSource.GamepadAxis`. \

### ⭐ Properties

#### Axis

```csharp
public Nullable<GamepadAxis> Axis { get; }
```

The bound gamepad analog axis, if `Source` is `InputSource.GamepadAxis`; otherwise `null`.

**Returns** \
[GamepadAxis?](../../../Murder/Core/Input/GamepadAxis.html) \

#### Gamepad

```csharp
public Nullable<Buttons> Gamepad { get; }
```

The bound gamepad button, if `Source` is `InputSource.Gamepad`; otherwise `null`.

**Returns** \
[Buttons?](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Buttons.html) \

#### Keyboard

```csharp
public Nullable<Keys> Keyboard { get; }
```

The bound keyboard key, if `Source` is `InputSource.Keyboard`; otherwise `null`.

**Returns** \
[Keys?](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Keys.html) \

#### Mouse

```csharp
public Nullable<MouseButtons> Mouse { get; }
```

The bound mouse button, if `Source` is `InputSource.Mouse`; otherwise `null`.

**Returns** \
[MouseButtons?](../../../Murder/Core/Input/MouseButtons.html) \

#### Source

```csharp
public readonly InputSource Source;
```

The device family this binding reads from. Determines which of `Keyboard`, `Gamepad`, `Mouse` or `Axis` is populated.

**Returns** \
[InputSource](../../../Murder/Core/Input/InputSource.html) \

### ⭐ Methods

#### ButtonToAxis(bool, bool, bool, bool)

```csharp
public Vector2 ButtonToAxis(bool up, bool right, bool left, bool down)
```

Converts four independent directional booleans (e.g. the four D-pad directions) into a single 2D vector with each axis in [-1, 1]. Opposite directions held simultaneously cancel out.

**Parameters** \
`up` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
Whether the "up" direction is currently held. \
`right` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
Whether the "right" direction is currently held. \
`left` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
Whether the "left" direction is currently held. \
`down` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
Whether the "down" direction is currently held. \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
A vector whose X is -1/0/1 for left/none/right and whose Y is -1/0/1 for up/none/down. \

#### Check(InputState)

```csharp
public bool Check(InputState state)
```

Returns whether this binding is currently held down, reading the appropriate part of `state` based on `Source`. Mouse buttons are ignored while the game window is not active (`Game.IsActive` is `false`) so alt-tabbing does not leave a click "stuck". This is the core per-frame poll used by `VirtualButton.Update`.

**Parameters** \
`state` [InputState](../../../Murder/Core/Input/InputState.html) \
The raw input snapshot for the current frame. \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`true` if the bound key/button is currently pressed. \

#### Equals(InputButton)

```csharp
public bool Equals(InputButton other)
```

Compares two bindings by their underlying key/button/mouse/axis values (not by `Source` directly, though in practice only one of the four is non-null at a time).

**Parameters** \
`other` [InputButton](../../../Murder/Core/Input/InputButton.html) \
The other binding to compare against. \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`true` if both bindings refer to the same physical control. \

#### GetAxis(GamePadState)

```csharp
public Vector2 GetAxis(GamePadState gamepadState)
```

Reads the current 2D value of this binding when it is a `InputSource.GamepadAxis` binding — the left/right thumbstick value (Y inverted so up is positive), or the D-pad converted to a directional vector via `ButtonToAxis`. Returns `Vector2.Zero` for any other `Source`. Used by `InputButtonAxis.Check` for its single-axis case.

**Parameters** \
`gamepadState` [GamePadState](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.GamePadState.html) \
The raw gamepad state to read the axis from. \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
The current axis value, or `Vector2.Zero` if this binding is not a gamepad axis. \

**Exceptions** \
[Exception](https://learn.microsoft.com/en-us/dotnet/api/System.Exception?view=net-7.0) \
Thrown if bound to a `GamepadAxis` value that has no supported mapping. \

#### GetInputImageStyle()

```csharp
public InputImageStyle GetInputImageStyle()
```

Maps this binding to the `InputImageStyle` that identifies which icon/glyph the UI should render for it (e.g. a specific gamepad face-button shape, or a wide vs. narrow key cap). Used by prompt/HUD rendering code to show the player which physical control to press.

**Returns** \
[InputImageStyle](../../../Murder/Core/Input/InputImageStyle.html) \
The icon style that best represents this binding's physical control. \

#### IsAvailable(GamePadCapabilities)

```csharp
public bool IsAvailable(GamePadCapabilities capabilities)
```

Returns whether this binding's physical control actually exists on the given gamepad — used to filter which bindings should be advertised/allowed, e.g. skip a gamepad binding entirely when no controller is connected. Keyboard and mouse bindings are always considered available.

**Parameters** \
`capabilities` [GamePadCapabilities](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.GamePadCapabilities.html) \
The capabilities of the gamepad to check against, from `GamePad.GetCapabilities`. \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`true` if this binding can currently be triggered. \

#### ToString()

```csharp
public virtual string ToString()
```

Returns a human-readable representation of the bound key/button/mouse control, or `"<none>"`/`"?"` when unbound.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

⚡

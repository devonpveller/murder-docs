# InputButtonAxis

**Namespace:** Murder.Core.Input \
**Assembly:** Murder.dll

```csharp
public sealed struct InputButtonAxis
```

A set of four directional `InputButton` bindings (up/down/left/right) or a single analog axis that together form a 2D movement axis.

**Intent:** Represent a 2D movement axis built from directional buttons or a gamepad thumbstick.

**Use-case:** Construct an `InputButtonAxis` with WASD keys, D-pad buttons, or a `GamepadAxis` and pass it to `PlayerInput.Register(int axis, ...)` to drive a `VirtualAxis`.

### ⭐ Constructors
```csharp
public InputButtonAxis(Buttons up, Buttons left, Buttons down, Buttons right)
```

**Parameters** \
`up` [Buttons](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Buttons.html) \
`left` [Buttons](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Buttons.html) \
`down` [Buttons](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Buttons.html) \
`right` [Buttons](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Buttons.html) \

```csharp
public InputButtonAxis(Keys up, Keys left, Keys down, Keys right)
```

**Parameters** \
`up` [Keys](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Keys.html) \
`left` [Keys](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Keys.html) \
`down` [Keys](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Keys.html) \
`right` [Keys](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Keys.html) \

```csharp
public InputButtonAxis(GamepadAxis axis)
```

**Parameters** \
`axis` [GamepadAxis](../../../Murder/Core/Input/GamepadAxis.html) \

```csharp
public InputButtonAxis(InputButton up, InputButton left, InputButton down, InputButton right)
```

**Parameters** \
`up` [InputButton](../../../Murder/Core/Input/InputButton.html) \
`left` [InputButton](../../../Murder/Core/Input/InputButton.html) \
`down` [InputButton](../../../Murder/Core/Input/InputButton.html) \
`right` [InputButton](../../../Murder/Core/Input/InputButton.html) \

### ⭐ Properties
#### Down
```csharp
public readonly InputButton Down;
```

The button bound to the downward direction.

**Returns** \
[InputButton](../../../Murder/Core/Input/InputButton.html) \
#### Left
```csharp
public readonly InputButton Left;
```

The button bound to the leftward direction.

**Returns** \
[InputButton](../../../Murder/Core/Input/InputButton.html) \
#### Right
```csharp
public readonly InputButton Right;
```

The button bound to the rightward direction.

**Returns** \
[InputButton](../../../Murder/Core/Input/InputButton.html) \
#### Single
```csharp
public readonly T? Single;
```

When set, this axis uses a single analog `InputButton` (e.g. a thumbstick) instead of four directional buttons.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
#### Source
```csharp
public readonly InputSource Source;
```

The device source for this axis (keyboard, gamepad, etc.).

**Returns** \
[InputSource](../../../Murder/Core/Input/InputSource.html) \
#### Up
```csharp
public readonly InputButton Up;
```

The button bound to the upward direction.

**Returns** \
[InputButton](../../../Murder/Core/Input/InputButton.html) \
### ⭐ Methods
#### Check(InputState)
```csharp
public Vector2 Check(InputState state)
```

Returns the current axis vector from this binding given the raw `state`. Uses the analog value when `Single` is set, or a discrete ±1 vector from the four directional buttons.

**Parameters** \
`state` [InputState](../../../Murder/Core/Input/InputState.html) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### ToString()
```csharp
public virtual string ToString()
```

Returns a human-readable description of the active bindings in this axis.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \



⚡
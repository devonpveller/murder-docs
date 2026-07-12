# InputButtonAxis

**Namespace:** Murder.Core.Input \
**Assembly:** Murder.dll

```csharp
public sealed struct InputButtonAxis
```

A 2D movement/direction binding, built either from four independent `InputButton` directions (e.g. WASD or D-pad buttons) or from a single analog `InputButton` that reads a gamepad axis (a thumbstick).

**Intent:** Represent a 2D movement axis built from directional buttons or a single gamepad thumbstick, as the unit registered against a logical axis id.

**Use-case:** Construct an `InputButtonAxis` with WASD keys, D-pad buttons, or a `GamepadAxis` and pass it to `PlayerInput.Register(int axis, InputButtonAxis[] buttonAxes)` to drive a `VirtualAxis`. Polled every frame by `VirtualAxis.Update` to drive movement, menu navigation, and camera control.

### ⭐ Constructors

```csharp
public InputButtonAxis(Buttons up, Buttons left, Buttons down, Buttons right)
```

Builds a directional axis out of four digital gamepad buttons (e.g. the D-pad's four buttons).

**Parameters** \
`up` [Buttons](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Buttons.html) \
Button for the upward direction. \
`left` [Buttons](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Buttons.html) \
Button for the leftward direction. \
`down` [Buttons](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Buttons.html) \
Button for the downward direction. \
`right` [Buttons](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Buttons.html) \
Button for the rightward direction. \

```csharp
public InputButtonAxis(Keys up, Keys left, Keys down, Keys right)
```

Builds a directional axis out of four keyboard keys (e.g. W/A/S/D or the arrow keys).

**Parameters** \
`up` [Keys](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Keys.html) \
Key for the upward direction. \
`left` [Keys](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Keys.html) \
Key for the leftward direction. \
`down` [Keys](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Keys.html) \
Key for the downward direction. \
`right` [Keys](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Keys.html) \
Key for the rightward direction. \

```csharp
public InputButtonAxis(GamepadAxis axis)
```

Builds an analog axis that reads a single gamepad axis (a thumbstick, or the D-pad as an analog direction) instead of four discrete buttons.

**Parameters** \
`axis` [GamepadAxis](../../../Murder/Core/Input/GamepadAxis.html) \
The gamepad axis to read. \

```csharp
public InputButtonAxis(InputButton up, InputButton left, InputButton down, InputButton right)
```

Builds a directional axis out of four pre-built `InputButton` bindings.

**Parameters** \
`up` [InputButton](../../../Murder/Core/Input/InputButton.html) \
Binding for the upward direction. \
`left` [InputButton](../../../Murder/Core/Input/InputButton.html) \
Binding for the leftward direction. \
`down` [InputButton](../../../Murder/Core/Input/InputButton.html) \
Binding for the downward direction. \
`right` [InputButton](../../../Murder/Core/Input/InputButton.html) \
Binding for the rightward direction. \

### ⭐ Properties

#### Down

```csharp
public readonly InputButton Down;
```

The button bound to the downward direction. Ignored when `Single` is set.

**Returns** \
[InputButton](../../../Murder/Core/Input/InputButton.html) \

#### Left

```csharp
public readonly InputButton Left;
```

The button bound to the leftward direction. Ignored when `Single` is set.

**Returns** \
[InputButton](../../../Murder/Core/Input/InputButton.html) \

#### Right

```csharp
public readonly InputButton Right;
```

The button bound to the rightward direction. Ignored when `Single` is set.

**Returns** \
[InputButton](../../../Murder/Core/Input/InputButton.html) \

#### Single

```csharp
public readonly Nullable<InputButton> Single;
```

When set, this axis reads a single analog gamepad axis (see the `InputButtonAxis(GamepadAxis)` constructor) instead of the four directional buttons `Up`/`Left`/`Down`/`Right`.

**Returns** \
[InputButton?](../../../Murder/Core/Input/InputButton.html) \

#### Source

```csharp
public readonly InputSource Source;
```

The device family this axis reads from, taken from whichever constructor built it.

**Returns** \
[InputSource](../../../Murder/Core/Input/InputSource.html) \

#### Up

```csharp
public readonly InputButton Up;
```

The button bound to the upward direction. Ignored when `Single` is set.

**Returns** \
[InputButton](../../../Murder/Core/Input/InputButton.html) \

### ⭐ Methods

#### Check(InputState)

```csharp
public Vector2 Check(InputState state)
```

Reads the current 2D value of this axis for the given frame's `state`: the raw analog value when `Single` is set, or a discrete vector in [-1, 1] per component built from whichever of the four directional buttons are currently held. Called every frame by `VirtualAxis.Update` for each registered `InputButtonAxis`.

**Parameters** \
`state` [InputState](../../../Murder/Core/Input/InputState.html) \
The raw input snapshot for the current frame. \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
The current 2D direction/value of this axis. \

#### ToString()

```csharp
public virtual string ToString()
```

Returns a human-readable description of the active bindings in this axis — the single analog binding's description, or the four directional bindings joined together.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

⚡

# VirtualAxis

**Namespace:** Murder.Core.Input \
**Assembly:** Murder.dll

```csharp
public class VirtualAxis : IVirtualInput
```

Runtime state container for a 2D input axis — tracks value, direction, pressed/down state, and tick-repeat behaviour for one or more `InputButtonAxis`/`GamepadAxis` bindings.

**Intent:** Maintain the per-frame state of a logical 2D axis mapped to one or more `InputButtonAxis` bindings, decoupling gameplay/UI code from the specific physical sticks/keys the player has bound.

**Use-case:** Access via `PlayerInput.GetAxis(int)`/`GetOrCreateAxis(int)` (e.g. `Game.Input.GetAxis(MurderInputAxis.Ui)`). Check `Value`/`IntValue` for the current direction, `Pressed` for the first-frame press, and `Tick`/`TickX`/`TickY` for key-repeat navigation in menus — this is exactly how `PlayerInput.VerticalMenu`/`HorizontalMenu`/`GridMenu` drive cursor movement.

**Implements:** _[IVirtualInput](../../../Murder/Core/Input/IVirtualInput.html)_

### ⭐ Constructors

```csharp
public VirtualAxis()
```

Creates an empty axis with no bindings; call `Register(...)` (directly or via `PlayerInput.Register`/`RegisterAxes`) to add bindings before it can report any state.

### ⭐ Properties

#### \_lastPressedButton

```csharp
public InputButtonAxis?[] _lastPressedButton;
```

A 2-element array tracking the most recently active `InputButtonAxis` for keyboard/mouse input (index 1, when `Game.Input.UsingKeyboard` is `true`) and gamepad input (index 0). Backing store for `LastPressedAxes(bool)`.

**Returns** \
[InputButtonAxis?[]](../../../Murder/Core/Input/InputButtonAxis.html) \

#### ButtonAxis

```csharp
public ImmutableArray<InputButtonAxis> ButtonAxis { get; }
```

The set of `InputButtonAxis` bindings registered to this virtual axis, summed together every frame to produce `Value`.

**Returns** \
[ImmutableArray\<InputButtonAxis\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### Consumed

```csharp
public bool Consumed;
```

Whether this axis has been consumed for the current frame. Note that unlike `VirtualButton`, nothing in `VirtualAxis`/`PlayerInput` currently reads this flag to gate `Pressed`/`Value` — it is reset to `false` every `Update(InputState)` call but is otherwise informational; only `ConsumeAll()`/`Consume()` on `PlayerInput` set it.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Down

```csharp
public bool Down { get; private set; }
```

`true` while any bound `InputButtonAxis` reports a non-zero vector, recomputed every `Update(InputState)` call.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IntPreviousValue

```csharp
public Point IntPreviousValue { get; private set; }
```

The dominant-direction `IntValue` from the previous frame, used internally to detect a fresh directional press (`PressedX`/`PressedY`).

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### IntValue

```csharp
public Point IntValue { get; private set; }
```

A discretized version of `Value`: once the raw vector exceeds a 0.65 deadzone, this snaps to one of the 8 cardinal/diagonal directions (each component -1, 0 or 1). Menu navigation (`PlayerInput.VerticalMenu`/`HorizontalMenu`/`GridMenu`) reads this (via `Tick`) instead of the raw `Value` so a slightly-off-center stick still reads as a clean up/down/left/right.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### Pressed

```csharp
public bool Pressed { get; }
```

`true` for the single frame `IntValue` becomes non-zero and differs from `IntPreviousValue` while the axis is down — i.e. the frame a new dominant direction is registered.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### PressedValue

```csharp
public Point PressedValue { get; private set; }
```

Snapshot of `IntValue` taken the frame `Pressed` (or an externally-driven `Press(Vector2)`) fired; reset to `Point.Zero` on frames where the axis is not freshly pressed.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### PressedX

```csharp
public bool PressedX { get; }
```

`true` for the single frame the horizontal component of `IntValue` becomes non-zero and differs from `IntPreviousValue.X` while down.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### PressedY

```csharp
public bool PressedY { get; }
```

`true` for the single frame the vertical component of `IntValue` becomes non-zero and differs from `IntPreviousValue.Y` while down.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Previous

```csharp
public bool Previous { get; private set; }
```

`true` if the axis was down during the previous frame; used internally to derive `Pressed`/`Released`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### PreviousValue

```csharp
public Vector2 PreviousValue { get; private set; }
```

The raw `Value` from the previous frame, before the current frame's `Update`/`Press` recomputed it.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Tick

```csharp
public Point Tick { get; }
```

The key-repeat-gated version of `IntValue`: `X`/`Y` report `IntValue.X`/`IntValue.Y` only on the frame a repeat "tick" fires (the initial press, then every `_tickDelay` seconds after an initial `_firstTickDelay` hold), and `0` otherwise. This is what `PlayerInput.VerticalMenu`/`HorizontalMenu`/`GridMenu` read (via `TickX`/`TickY`) to move a menu cursor once per repeat step instead of every single frame the stick is held over.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### TickX

```csharp
public bool TickX { get; }
```

Like a keyboard key, true on pressed and then every `_tickDelay` seconds. First tick is after `_firstTickDelay`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TickY

```csharp
public bool TickY { get; }
```

Like a keyboard key, true on pressed and then every `_tickDelay` seconds. First tick is after `_firstTickDelay`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Value

```csharp
public Vector2 Value { get; private set; }
```

The raw, continuous axis value for this frame: the sum of every bound `InputButtonAxis`'s vector, clamped to unit length once its squared length exceeds 1, and zeroed out entirely below a small (0.15 squared) deadzone. Read this for analog movement; read `IntValue`/`Tick` instead for discrete/menu-style navigation.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

### ⭐ Events

#### OnPress

```csharp
public event Action<InputState> OnPress;
```

Fired during `Update(InputState)` on the frame `Pressed` becomes `true`.

**Returns** \
[Action\<InputState\>](https://learn.microsoft.com/en-us/dotnet/api/System.Action-1?view=net-7.0) \

### ⭐ Methods

#### GetActiveButtonDescriptions()

```csharp
public IEnumerable<string> GetActiveButtonDescriptions()
```

Enumerates the `ToString()` description of every registered `InputButtonAxis` binding. Used by input-remapping/help UI to list what's currently bound to this axis.

**Returns** \
[IEnumerable\<string\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \

#### LastPressedAxes(bool)

```csharp
public InputButtonAxis LastPressedAxes(bool keyboard)
```

Returns the last `InputButtonAxis` that was active, from keyboard/mouse (`keyboard=true`) or gamepad (`keyboard=false`). Falls back to the first registered binding matching that source (or the first binding overall) if nothing has been pressed yet.

**Parameters** \
`keyboard` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[InputButtonAxis](../../../Murder/Core/Input/InputButtonAxis.html) \

#### Press(Vector2)

```csharp
public void Press(Vector2 value)
```

Force-sets `Value` (and the derived `IntValue`/`Down`/tick state) to `value`, bypassing the physical device state entirely. This is what `PlayerInput.MockInput(int, Vector2)` calls under the hood, useful for automated tests, tutorials/scripted sequences, or simulating axis input from an unrelated source (e.g. a virtual on-screen joystick).

**Parameters** \
`value` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
The axis vector to force this frame.

#### Update(InputState)

```csharp
public virtual void Update(InputState inputState)
```

Recomputes `Value`, `IntValue`, `Down`, `Pressed`/`PressedX`/`PressedY`, `Tick`/`TickX`/`TickY` and the last-pressed tracking from `inputState` against every registered `InputButtonAxis`. Called once per frame by `PlayerInput.Update()` for every registered axis; game code should not normally call this directly.

**Parameters** \
`inputState` [InputState](../../../Murder/Core/Input/InputState.html) \

⚡

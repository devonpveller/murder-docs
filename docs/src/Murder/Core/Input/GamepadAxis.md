# GamepadAxis

**Namespace:** Murder.Core.Input \
**Assembly:** Murder.dll

```csharp
public sealed enum GamepadAxis : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Identifies a gamepad control that produces a continuous 2D value rather than a single on/off state.

**Intent:** Select an analog stick, or the D-pad treated as an analog direction, for input mapping — as opposed to a single digital `Buttons` value.

**Use-case:** Pass a `GamepadAxis` to the `InputButton(GamepadAxis)` or `InputButtonAxis(GamepadAxis)` constructors to bind an analog control to a virtual button or axis, or to `PlayerInput.RegisterAxes(int, GamepadAxis[])` / `RegisterAxesAsButton(int, GamepadAxis[])` to register it directly.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### Dpad

```csharp
public static const GamepadAxis Dpad;
```

The directional pad, read as a 2D axis (via `InputButton.GetAxis`) instead of four discrete buttons.

**Returns** \
[GamepadAxis](../../../Murder/Core/Input/GamepadAxis.html) \

#### LeftThumb

```csharp
public static const GamepadAxis LeftThumb;
```

The left analog thumbstick.

**Returns** \
[GamepadAxis](../../../Murder/Core/Input/GamepadAxis.html) \

#### RightThumb

```csharp
public static const GamepadAxis RightThumb;
```

The right analog thumbstick.

**Returns** \
[GamepadAxis](../../../Murder/Core/Input/GamepadAxis.html) \

⚡

# GamepadAxis

**Namespace:** Murder.Core.Input \
**Assembly:** Murder.dll

```csharp
public sealed enum GamepadAxis : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Identifies a gamepad analog axis.

**Intent:** Select a specific analog stick or D-pad axis for input mapping.

**Use-case:** Pass a `GamepadAxis` to `InputButton` or `InputButtonAxis` constructors to bind an axis-based input to a virtual button or axis action.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties
#### Dpad
```csharp
public static const GamepadAxis Dpad;
```

The directional pad treated as a 2D axis.

**Returns** \
[GamepadAxis](../../../Murder/Core/Input/GamepadAxis.html) \
#### LeftThumb
```csharp
public static const GamepadAxis LeftThumb;
```

The left thumbstick axis.

**Returns** \
[GamepadAxis](../../../Murder/Core/Input/GamepadAxis.html) \
#### RightThumb
```csharp
public static const GamepadAxis RightThumb;
```

The right thumbstick axis.

**Returns** \
[GamepadAxis](../../../Murder/Core/Input/GamepadAxis.html) \


⚡
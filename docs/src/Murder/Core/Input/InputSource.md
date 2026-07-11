# InputSource

**Namespace:** Murder.Core.Input \
**Assembly:** Murder.dll

```csharp
public sealed enum InputSource : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Identifies which input device an `InputButton` or `InputButtonAxis` originates from.

**Intent:** Distinguish the physical source of an input binding.

**Use-case:** Check `InputButton.Source` to determine whether the player is using keyboard/mouse or a gamepad, enabling the UI to show the correct button prompt.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties
#### Gamepad
```csharp
public static const InputSource Gamepad;
```

A digital gamepad button.

**Returns** \
[InputSource](../../../Murder/Core/Input/InputSource.html) \
#### GamepadAxis
```csharp
public static const InputSource GamepadAxis;
```

A gamepad analog axis (thumbstick or D-pad treated as analog).

**Returns** \
[InputSource](../../../Murder/Core/Input/InputSource.html) \
#### Keyboard
```csharp
public static const InputSource Keyboard;
```

A keyboard key.

**Returns** \
[InputSource](../../../Murder/Core/Input/InputSource.html) \
#### Mouse
```csharp
public static const InputSource Mouse;
```

A mouse button.

**Returns** \
[InputSource](../../../Murder/Core/Input/InputSource.html) \
#### None
```csharp
public static const InputSource None;
```

No input source assigned (default / unbound state).

**Returns** \
[InputSource](../../../Murder/Core/Input/InputSource.html) \


⚡
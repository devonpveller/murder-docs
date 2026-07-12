# InputSource

**Namespace:** Murder.Core.Input \
**Assembly:** Murder.dll

```csharp
public sealed enum InputSource : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Identifies the physical device family that an `InputButton` or `InputButtonAxis` binding reads from.

**Intent:** Distinguish the physical source of an input binding so the right part of an `InputState` snapshot is inspected.

**Use-case:** Every binding records its `InputSource` so `InputButton.Check` knows which part of `InputState` to read; check `InputButton.Source` to determine whether the player is using keyboard/mouse or a gamepad, enabling the UI to show the correct button prompt.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### Gamepad

```csharp
public static const InputSource Gamepad;
```

A digital gamepad button, checked against `InputState.GamePadState`.

**Returns** \
[InputSource](../../../Murder/Core/Input/InputSource.html) \

#### GamepadAxis

```csharp
public static const InputSource GamepadAxis;
```

An analog gamepad axis (thumbstick or D-pad treated as analog) rather than a discrete button.

**Returns** \
[InputSource](../../../Murder/Core/Input/InputSource.html) \

#### Keyboard

```csharp
public static const InputSource Keyboard;
```

A keyboard key, checked against `InputState.KeyboardState`.

**Returns** \
[InputSource](../../../Murder/Core/Input/InputSource.html) \

#### Mouse

```csharp
public static const InputSource Mouse;
```

A mouse button, checked against `InputState.MouseState`.

**Returns** \
[InputSource](../../../Murder/Core/Input/InputSource.html) \

#### None

```csharp
public static const InputSource None;
```

No device assigned; the default/unbound state.

**Returns** \
[InputSource](../../../Murder/Core/Input/InputSource.html) \

⚡

# InputImageStyle

**Namespace:** Murder.Core.Input \
**Assembly:** Murder.dll

```csharp
public sealed enum InputImageStyle : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Identifies which icon/glyph should be shown in the UI for a given `InputButton`.

**Intent:** Let prompt/HUD rendering code look up the matching sprite (e.g. an Xbox "A" glyph, a keyboard key cap, a mouse-click icon) for a binding without inspecting its specific `Keys`, `Buttons`, or `MouseButtons` value.

**Use-case:** Call `InputButton.GetInputImageStyle()` to get the style for a binding, then look up the corresponding sprite in your UI atlas to render contextual button prompts (e.g. "Press [A] to interact").

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### GamepadButtonEast

```csharp
public static const InputImageStyle GamepadButtonEast;
```

The "east" gamepad face button (B on Xbox, Circle on PlayStation).

**Returns** \
[InputImageStyle](../../../Murder/Core/Input/InputImageStyle.html) \

#### GamepadButtonGeneric

```csharp
public static const InputImageStyle GamepadButtonGeneric;
```

A gamepad face button with no specific glyph mapping (fallback).

**Returns** \
[InputImageStyle](../../../Murder/Core/Input/InputImageStyle.html) \

#### GamepadButtonNorth

```csharp
public static const InputImageStyle GamepadButtonNorth;
```

The "north" gamepad face button (Y on Xbox, Triangle on PlayStation).

**Returns** \
[InputImageStyle](../../../Murder/Core/Input/InputImageStyle.html) \

#### GamepadButtonSouth

```csharp
public static const InputImageStyle GamepadButtonSouth;
```

The "south" gamepad face button (A on Xbox, Cross on PlayStation).

**Returns** \
[InputImageStyle](../../../Murder/Core/Input/InputImageStyle.html) \

#### GamepadButtonWest

```csharp
public static const InputImageStyle GamepadButtonWest;
```

The "west" gamepad face button (X on Xbox, Square on PlayStation).

**Returns** \
[InputImageStyle](../../../Murder/Core/Input/InputImageStyle.html) \

#### GamepadDPad

```csharp
public static const InputImageStyle GamepadDPad;
```

The directional pad as a whole, used when the binding is a `GamepadAxis.Dpad` axis rather than an individual direction.

**Returns** \
[InputImageStyle](../../../Murder/Core/Input/InputImageStyle.html) \

#### GamepadDPadDown

```csharp
public static const InputImageStyle GamepadDPadDown;
```

The down direction of the directional pad.

**Returns** \
[InputImageStyle](../../../Murder/Core/Input/InputImageStyle.html) \

#### GamepadDPadLeft

```csharp
public static const InputImageStyle GamepadDPadLeft;
```

The left direction of the directional pad.

**Returns** \
[InputImageStyle](../../../Murder/Core/Input/InputImageStyle.html) \

#### GamepadDPadRight

```csharp
public static const InputImageStyle GamepadDPadRight;
```

The right direction of the directional pad.

**Returns** \
[InputImageStyle](../../../Murder/Core/Input/InputImageStyle.html) \

#### GamepadDPadUp

```csharp
public static const InputImageStyle GamepadDPadUp;
```

The up direction of the directional pad.

**Returns** \
[InputImageStyle](../../../Murder/Core/Input/InputImageStyle.html) \

#### GamepadExtra

```csharp
public static const InputImageStyle GamepadExtra;
```

A miscellaneous gamepad control (Start, Back/Select, or the guide/big button).

**Returns** \
[InputImageStyle](../../../Murder/Core/Input/InputImageStyle.html) \

#### GamepadLeftShoulder

```csharp
public static const InputImageStyle GamepadLeftShoulder;
```

The left shoulder button or left trigger.

**Returns** \
[InputImageStyle](../../../Murder/Core/Input/InputImageStyle.html) \

#### GamepadRightShoulder

```csharp
public static const InputImageStyle GamepadRightShoulder;
```

The right shoulder button or right trigger.

**Returns** \
[InputImageStyle](../../../Murder/Core/Input/InputImageStyle.html) \

#### GamepadStick

```csharp
public static const InputImageStyle GamepadStick;
```

A thumbstick, used for both the left and right stick bindings.

**Returns** \
[InputImageStyle](../../../Murder/Core/Input/InputImageStyle.html) \

#### Keyboard

```csharp
public static const InputImageStyle Keyboard;
```

A regular, single-character keyboard key (rendered as a small key cap).

**Returns** \
[InputImageStyle](../../../Murder/Core/Input/InputImageStyle.html) \

#### KeyboardLong

```csharp
public static const InputImageStyle KeyboardLong;
```

A keyboard key whose label is long (e.g. Tab, Enter, Space, Esc), rendered as a wider key cap.

**Returns** \
[InputImageStyle](../../../Murder/Core/Input/InputImageStyle.html) \

#### MouseExtra

```csharp
public static const InputImageStyle MouseExtra;
```

Any other mouse button not covered by the other mouse values.

**Returns** \
[InputImageStyle](../../../Murder/Core/Input/InputImageStyle.html) \

#### MouseLeft

```csharp
public static const InputImageStyle MouseLeft;
```

The left mouse button.

**Returns** \
[InputImageStyle](../../../Murder/Core/Input/InputImageStyle.html) \

#### MouseMiddle

```csharp
public static const InputImageStyle MouseMiddle;
```

The middle mouse button (scroll-wheel click).

**Returns** \
[InputImageStyle](../../../Murder/Core/Input/InputImageStyle.html) \

#### MouseRight

```csharp
public static const InputImageStyle MouseRight;
```

The right mouse button.

**Returns** \
[InputImageStyle](../../../Murder/Core/Input/InputImageStyle.html) \

#### MouseWheel

```csharp
public static const InputImageStyle MouseWheel;
```

The mouse scroll wheel.

**Returns** \
[InputImageStyle](../../../Murder/Core/Input/InputImageStyle.html) \

#### None

```csharp
public static const InputImageStyle None;
```

No binding, or the binding does not map to a displayable icon.

**Returns** \
[InputImageStyle](../../../Murder/Core/Input/InputImageStyle.html) \

⚡

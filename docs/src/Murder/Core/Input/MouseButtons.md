# MouseButtons

**Namespace:** Murder.Core.Input \
**Assembly:** Murder.dll

```csharp
public sealed enum MouseButtons : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Identifies the mouse buttons supported as input bindings.

**Intent:** Select a specific mouse button for use in `InputButton` bindings.

**Use-case:** Pass a `MouseButtons` value to `PlayerInput.RegisterButton(int, MouseButtons[])`/`PlayerInput.Register(int, MouseButtons[])` to bind a logical button id (e.g. `MurderInputButtons.LeftClick`) to a physical mouse click, or read `PlayerInput.GetAnyMouseButton()` to discover which button (if any) is currently pressed. The engine itself uses this to wire up `MurderInputButtons.LeftClick`/`RightClick`/`MiddleClick` during `Game.Initialize()`.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### Left

```csharp
public static const MouseButtons Left;
```

The left (primary) mouse button.

**Returns** \
[MouseButtons](../../../Murder/Core/Input/MouseButtons.html) \

#### Middle

```csharp
public static const MouseButtons Middle;
```

The middle mouse button (scroll wheel click).

**Returns** \
[MouseButtons](../../../Murder/Core/Input/MouseButtons.html) \

#### Right

```csharp
public static const MouseButtons Right;
```

The right (secondary) mouse button.

**Returns** \
[MouseButtons](../../../Murder/Core/Input/MouseButtons.html) \

⚡

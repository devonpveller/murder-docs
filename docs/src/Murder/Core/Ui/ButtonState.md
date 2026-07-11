# ButtonState

**Namespace:** Murder.Core.Ui \
**Assembly:** Murder.dll

```csharp
sealed enum ButtonState : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Describes the current interaction state of a `SimpleButton`.

**Intent:** Enum that tracks whether a button is inactive, hovered, held down, or disabled so the rendering code can apply the correct visual style.

**Use-case:** Checked by `SimpleButton.Draw` to select which sprite frame to render, and updated by `SimpleButton.Update` each frame based on cursor input.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties
#### Disabled
```csharp
public static const ButtonState Disabled;
```

The button is not interactive and is rendered in a visually disabled style.

**Returns** \
[ButtonState](../../../Murder/Core/Ui/ButtonState.html) \
#### Down
```csharp
public static const ButtonState Down;
```

The button is being pressed (cursor is over it and the click input is held).

**Returns** \
[ButtonState](../../../Murder/Core/Ui/ButtonState.html) \
#### Hover
```csharp
public static const ButtonState Hover;
```

The cursor is hovering over the button but no click is in progress.

**Returns** \
[ButtonState](../../../Murder/Core/Ui/ButtonState.html) \
#### Normal
```csharp
public static const ButtonState Normal;
```

The button is idle — the cursor is not over it and it is not being clicked.

**Returns** \
[ButtonState](../../../Murder/Core/Ui/ButtonState.html) \


⚡
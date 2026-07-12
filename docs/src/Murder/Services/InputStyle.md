# InputStyle

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public enum InputStyle : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Identifies what kind of binding an [InputMenuOption](../../Murder/Services/InputMenuOption.html) represents. Declared as a nested type of `InputMenuOption`.

**Intent:** Lets the rebinding-menu UI dispatch on entry type — a regular button, an axis (analogue or digital), or one of the special non-binding entries (swap submit/cancel, allow mouse clicks) — without inspecting the entry's label text.

**Use-case:** Read via `InputMenuOption.Style` when handling a selection in the controls-rebinding menu to decide whether to start listening for a button press, an axis input, or to toggle a setting instead.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### None

```csharp
public static const InputStyle None;
```

The entry is not tied to a rebindable input at all (used for the "reset" and "exit" menu entries).

**Returns** \
[InputStyle](../../Murder/Services/InputStyle.html) \

#### Button

```csharp
public static const InputStyle Button;
```

The entry rebinds a single digital button.

**Returns** \
[InputStyle](../../Murder/Services/InputStyle.html) \

#### AxisAnalogue

```csharp
public static const InputStyle AxisAnalogue;
```

The entry rebinds an analogue axis. Currently unused by `InputServices.CreateBindingsMenuInfo`, which only builds digital-press axis entries.

**Returns** \
[InputStyle](../../Murder/Services/InputStyle.html) \

#### AxisDigitalPress

```csharp
public static const InputStyle AxisDigitalPress;
```

The entry rebinds an axis that is read as a digital press (e.g. a directional key mapped onto an axis) rather than an analogue value.

**Returns** \
[InputStyle](../../Murder/Services/InputStyle.html) \

#### SwapSubmitAndCancel

```csharp
public static const InputStyle SwapSubmitAndCancel;
```

Special entry that toggles whether the submit and cancel buttons are swapped, rather than rebinding a specific input.

**Returns** \
[InputStyle](../../Murder/Services/InputStyle.html) \

#### AllowMouseClicks

```csharp
public static const InputStyle AllowMouseClicks;
```

Special entry that toggles whether mouse clicks are accepted as submit/cancel input, rather than rebinding a specific input.

**Returns** \
[InputStyle](../../Murder/Services/InputStyle.html) \

⚡

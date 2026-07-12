# InputMenuOption

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public readonly struct InputMenuOption
```

Represents a single entry in a control-rebinding menu, pairing a display label with the button/axis id it controls and the kind of binding it represents.

**Intent:** Gives the rebinding menu UI enough information per entry to both render a label and know what to do when it's selected (rebind a button, rebind an axis, or trigger a special action like resetting all bindings), without the UI needing to understand raw button/axis ids directly.

**Use-case:** Built by [InputServices](../../Murder/Services/InputServices.html)`.CreateBindingsMenuInfo` — one instance per customizable button/axis, plus special entries (swap submit/cancel, allow mouse, reset, exit) — and consumed by the settings-menu rendering/interaction code, which reads `Style` to decide how to handle a selection and `Id` to know which button/axis to rebind.

### ⭐ Constructors

```csharp
public InputMenuOption(string text, InputStyle style, int? buttonId)
```

Creates a menu entry labeled `text`, tagged with `style` to describe what kind of binding it represents, and referencing `buttonId` (the button/axis id to rebind, or `null` for entries that aren't tied to a specific binding, like "reset" or "exit").

**Parameters** \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`style` [InputStyle](../../Murder/Services/InputStyle.html) \
`buttonId` [int?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

### ⭐ Properties

#### Id

```csharp
public readonly int? Id { get; init; }
```

The button or axis id this entry controls, or `null` for entries not tied to a specific binding (e.g. "reset all", "exit").

**Returns** \
[int?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### Style

```csharp
public readonly InputStyle Style { get; init; }
```

The kind of binding this entry represents, used by the menu's selection handler to decide how to react (start listening for a button press, start listening for an axis, toggle a setting, etc.).

**Returns** \
[InputStyle](../../Murder/Services/InputStyle.html) \

#### Text

```csharp
public readonly string Text { get; init; }
```

The localized/display label shown for this menu entry.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

⚡

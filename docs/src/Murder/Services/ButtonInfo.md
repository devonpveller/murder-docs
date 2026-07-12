# ButtonInfo

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public struct ButtonInfo
```

Style/layout data for drawing one or more prompt buttons (e.g. "Press A to continue") in the UI. Declared as a nested type of [MurderUiServices](../../Murder/Services/MurderUiServices.html).

**Intent:** Bundles the button sprite, label text (or list of labels for multi-button prompts), and colors needed to draw an input-prompt button, optionally paired with a `MenuInfo` when several buttons need to be presented and navigated as a group.

**Use-case:** Configure a `ButtonInfo` and pass it to the button-drawing routines in `MurderUiServices` to render an interaction/continue prompt tied to a specific input button — e.g. showing the current gamepad button icon plus label text over an interactable object or dialogue box.

### ⭐ Constructors

```csharp
public ButtonInfo()
```

Creates a `ButtonInfo` with default optional values: an empty `ButtonsText` list, no `MenuInfo`, and `IsButtonValid` set to `false`. The required fields (`Sprite`, `ButtonTextColor`, `ButtonBorderColor`) have no default and must be set explicitly.

### ⭐ Properties

#### ButtonBorderColor

```csharp
public Color ButtonBorderColor { get; init; }
```

Color of the button glyph's border/outline.

**Returns** \
[Color](../../Murder/Core/Graphics/Color.html) \

#### ButtonsText

```csharp
public IList<string> ButtonsText { get; init; }
```

The label(s) to display alongside the button glyph. When multiple buttons are displayed together (see `MenuInfo`), this holds one label per button.

**Returns** \
[IList\<string\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IList-1?view=net-7.0) \

#### ButtonTextColor

```csharp
public Color ButtonTextColor { get; init; }
```

Color of the button's label text.

**Returns** \
[Color](../../Murder/Core/Graphics/Color.html) \

#### IsButtonValid

```csharp
public bool IsButtonValid { get; init; }
```

Whether the button prompt currently represents a valid, actionable input (e.g. the referenced binding actually exists). Defaults to `false`; drawing code can use this to skip or gray out prompts for unbound/invalid inputs.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### MenuInfo

```csharp
public MenuInfo? MenuInfo { get; init; }
```

Optional [MenuInfo](../../Murder/Core/Input/MenuInfo.html) used when multiple buttons are displayed together as a navigable group, rather than a single standalone prompt.

**Returns** \
[MenuInfo?](../../Murder/Core/Input/MenuInfo.html) \

#### Sprite

```csharp
public Guid Sprite { get; init; }
```

GUID of the sprite asset used to draw the button glyph/icon.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

⚡

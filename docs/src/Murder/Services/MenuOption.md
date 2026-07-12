# MenuOption

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public sealed struct MenuOption
```

Represents a single selectable item in a menu drawn by `RenderServices.DrawVerticalMenu`.

**Intent:** Holds the display text and interaction state (enabled, faded, whether it plays a click sound) for one row of a rendered menu, independent of any input-handling logic.

**Use-case:** Build an array of `MenuOption` values (directly, or from plain strings via `MenuInfo`'s string-array constructors) and wrap them in a `MenuInfo`, then pass that to `RenderServices.DrawVerticalMenu` to render an interactive list with correctly enabled/faded rows. Set `Enabled` to `false` for options that exist but cannot currently be chosen, and `Faded` to visually de-emphasize an option without disabling it.

### ⭐ Constructors

```csharp
public MenuOption()
```

Creates an empty, enabled, faded option with no text. Rarely used directly; `MenuInfo`'s array-resizing helpers use this to pre-fill an options array before assigning text.

```csharp
public MenuOption(bool selectable)
```

Creates an empty option whose `Enabled` state is set to `selectable`, leaving `Text` blank. Used when the option's label will be filled in separately or is not text-based.

**Parameters** \
`selectable` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

```csharp
public MenuOption(string text, bool selectable = true)
```

The most common way to create an option: sets the visible `Text` and whether it can be selected, defaulting to selectable. This is what `MenuInfo`'s constructors use when building a menu from an array of plain strings.

**Parameters** \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`selectable` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

### ⭐ Properties

#### Enabled

```csharp
public bool Enabled { get; }
```

When `true` (the default), the item can be navigated to and selected by the player. When `false`, `RenderServices.DrawVerticalMenu` renders it in the "disabled" color (`DrawMenuStyle.Shadow`, with no outline) and menu navigation logic (see `MenuInfo`) skips over it. Set via the constructor; init-only, so create a new `MenuOption` to change it.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Faded

```csharp
public bool Faded { get; }
```

When `true` (the default), marks the option as visually faded/inactive. This is a presentation hint distinct from `Enabled` — a faded option can still be selectable — intended for menus that want to dim options contextually (for example, an item the player owns zero of) without fully disabling them. Init-only; set through the constructor.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Length

```csharp
public int Length { get; }
```

Length of the option's `Text` (`0` if `Text` is `null`). Convenience accessor used when measuring or laying out menu labels without a separate null check.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### SoundOnClick

```csharp
public bool SoundOnClick;
```

When `true` (the default), selecting this option should play the menu's submit/click sound. This is a mutable public field (not init-only), so it can be toggled after construction — for example to silence the sound for a "back" option that closes the menu instantly.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Text

```csharp
public string Text { get; }
```

The display label shown for this menu item. Empty by default; set through the constructor.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

⚡

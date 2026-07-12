# InputHelpers

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public static class InputHelpers
```

Utilities for text fitting, line counting, D-pad slot label formatting, and OS-aware keyboard modifier selection used by input display and text-entry systems.

**Intent:** Provides helpers for measuring and trimming text within a pixel width, converting numeric input slot indices to display strings, and picking the correct platform-specific "action" modifier key (Cmd on macOS, Ctrl elsewhere).

**Use-case:** Use `FitToWidth` and `GetAmountOfLines` for dialogue/UI text layout, `IntToDPad` to render controller button labels, `Clamp` to enforce a max length while the player is typing, and `OSActionModifier` for keyboard shortcuts that should follow platform convention (copy/paste, save, etc.) instead of hardcoding Ctrl.

### ⭐ Properties

#### OSActionModifier

```csharp
public static Keys OSActionModifier { get; }
```

The keyboard modifier key that represents the platform's primary "action" modifier: Cmd (mapped to `Keys.LeftWindows`) on macOS, or Left Ctrl on every other platform. Use instead of hardcoding `Keys.LeftControl` for shortcuts that should follow platform convention.

**Returns** \
[Keys](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Keys.html) \

### ⭐ Methods

#### FitToWidth(ReadOnlySpan`1&, int)

```csharp
public bool FitToWidth(ReadOnlySpan`1& text, int width)
```

Repeatedly trims one character off the end of `text` until its measured pixel width is no greater than `width`. Returns `true` if any trimming occurred. Use for fitting a single line of text (e.g. a truncated label) into a fixed-width UI element — this trims from the end rather than word-wrapping onto multiple lines.

**Parameters** \
`text` [ReadOnlySpan\<T\>&](https://learn.microsoft.com/en-us/dotnet/api/System.ReadOnlySpan-1?view=net-7.0) \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### GetAmountOfLines(ReadOnlySpan<T>, int)

```csharp
public int GetAmountOfLines(ReadOnlySpan<T> text, int width)
```

Estimates the number of display lines `text` would occupy if rendered at `width` pixels wide, based on its total measured pixel width divided by `width`. This is an approximation (total width ÷ target width), not an actual word-wrap simulation.

**Parameters** \
`text` [ReadOnlySpan\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.ReadOnlySpan-1?view=net-7.0) \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### IntToDPad(int)

```csharp
public string IntToDPad(int slot)
```

Converts a numeric D-pad slot index (0-3) to its corresponding button label string (`"D-Down"`, `"D-Left"`, `"D-Up"`, `"D-Right"`); any other value falls back to `"D-Down"`.

**Parameters** \
`slot` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Clamp(int)

```csharp
public void Clamp(int length)
```

Clamps the game's current text-input buffer (`Game.Input`) to at most `length` characters. Use while handling text-entry input to enforce a maximum field length as the player types.

**Parameters** \
`length` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡

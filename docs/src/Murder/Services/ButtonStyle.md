# ButtonStyle

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public readonly struct ButtonStyle
```

Defines the visual appearance of an interactive button drawn by the UI system: its background sprite, label font/color, and optional outline/shadow treatments.

**Intent:** Bundles all style parameters a button-drawing routine needs into a single value that can be authored once (often via the editor, since most properties carry `[PaletteColor]`/`[Font]`/`[Slider]` attributes for inspector UI) and reused across every button of a given visual style.

**Use-case:** Construct (or expose as an editable asset field) a `ButtonStyle` and pass it to the button-drawing helpers in [MurderUiServices](../../Murder/Services/MurderUiServices.html) to control how a menu button looks — its background `Portrait`, label alignment and color, optional text outline/shadow, and extra horizontal padding.

### ⭐ Constructors

```csharp
public ButtonStyle()
```

Creates a `ButtonStyle` with the struct's default values: an empty `Portrait` for `Sprite`, white `TextColor`, no outline/shadow colors, and zeroed padding. Because `ButtonStyle` is a `readonly struct` with `init`-only properties, use object initializer syntax (`new ButtonStyle { TextColor = ... }`) to customize it at construction time.

### ⭐ Properties

#### ExtraPaddingRight

```csharp
public readonly int ExtraPaddingRight { get; init; }
```

Additional pixels of padding added specifically on the right side of the button content area, on top of `ExtraPaddingX`. Use this to compensate for asymmetric button art or to make room for a trailing icon/indicator.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### ExtraPaddingX

```csharp
public readonly Point ExtraPaddingX { get; init; }
```

Extra horizontal padding added on both sides of the button content area, added to the intrinsic padding of the background sprite.

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### Font

```csharp
public readonly int Font;
```

Index of the font used for the button label, tagged with `[Font]` so it can be picked from the engine's font list in the editor. This is a plain field (not `init`), so it is set via object-initializer syntax like the other members but has no default other than `0`.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### OutlineColor

```csharp
public readonly Color? OutlineColor { get; init; }
```

Optional color for the button's border/background outline; `null` (the default) means no outline is drawn. Tagged `[PaletteColor]` so the editor can offer a palette picker.

**Returns** \
[Color?](../../Murder/Core/Graphics/Color.html) \

#### Sprite

```csharp
public readonly Portrait Sprite { get; init; }
```

The [Portrait](../../Murder/Core/Portrait.html) (sprite plus animation state) used as the button's background art.

**Returns** \
[Portrait](../../Murder/Core/Portrait.html) \

#### TextAlignment

```csharp
public readonly float TextAlignment { get; init; }
```

Horizontal alignment of the button label text in the range `[0, 1]`, where `0` is left-aligned and `1` is right-aligned; tagged `[Slider(0, 1)]` for editor use. Defaults to `0`.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### TextColor

```csharp
public readonly Color TextColor { get; init; }
```

Color of the button label text. Defaults to `Color.White`.

**Returns** \
[Color](../../Murder/Core/Graphics/Color.html) \

#### TextOutlineColor

```csharp
public readonly Color? TextOutlineColor { get; init; }
```

Optional color for a stroke drawn around the text glyphs; `null` (the default) means no text outline is drawn.

**Returns** \
[Color?](../../Murder/Core/Graphics/Color.html) \

#### TextShadowColor

```csharp
public readonly Color? TextShadowColor { get; init; }
```

Optional color for a drop shadow drawn beneath the button label; `null` (the default) means no shadow is drawn.

**Returns** \
[Color?](../../Murder/Core/Graphics/Color.html) \

⚡

# DrawMenuStyle

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public readonly struct DrawMenuStyle
```

Holds visual style parameters for drawing a vertical menu via `RenderServices.DrawVerticalMenu`.

**Intent:** Bundles font, color, alignment, animation, and spacing settings for rendered menus into a single value, so a menu's look can be authored once and passed by `in` reference to the draw call instead of threading a dozen separate parameters through it.

**Use-case:** Create and configure a `DrawMenuStyle` instance (typically as a static/cached value or an editor-exposed field), then pass it to `RenderServices.DrawVerticalMenu` alongside a `MenuInfo`/array of [MenuOption](../../Murder/Services/MenuOption.html) items to control how the list is rendered — colors for selected vs. unselected items, cursor animation timing/easing, and layout origin/spacing.

### ⭐ Constructors

```csharp
public DrawMenuStyle()
```

Creates a `DrawMenuStyle` with the struct's built-in defaults: origin `(0.5, 0)` (top-center pivot), `MurderFonts.LargeFont`, `Color.White` for the selected item, `Color.ColdGray` for unselected items, `Color.Black` for the shadow, and `2` extra pixels of vertical spacing between items. Since all properties are `init`-only, use object-initializer syntax (`new DrawMenuStyle { Font = ... }`) to override individual values.

### ⭐ Properties

#### Color

```csharp
public Color Color { get; init; }
```

Color used to render unselected menu items. Defaults to `Color.ColdGray`.

**Returns** \
[Color](../../Murder/Core/Graphics/Color.html) \

#### Ease

```csharp
public EaseKind Ease { get; init; }
```

Easing function applied to the selection cursor's movement animation as it travels between menu items.

**Returns** \
[EaseKind](../../Murder/Utilities/EaseKind.html) \

#### ExtraVerticalSpace

```csharp
public int ExtraVerticalSpace { get; init; }
```

Additional pixel spacing inserted between each menu item, on top of the font's natural line height. Defaults to `2`.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Font

```csharp
public int Font { get; init; }
```

Index of the font used to draw menu item text, tagged with `[Font]` for editor selection. Defaults to `MurderFonts.LargeFont`.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Origin

```csharp
public Vector2 Origin { get; init; }
```

Normalised origin point (pivot) for the menu layout, e.g. `(0.5, 0)` centers the menu horizontally with items growing downward from the top. Defaults to `(0.5, 0)`.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### SelectedColor

```csharp
public Color SelectedColor { get; init; }
```

Color used to render the currently selected menu item. Defaults to `Color.White`.

**Returns** \
[Color](../../Murder/Core/Graphics/Color.html) \

#### SelectorMoveTime

```csharp
public float SelectorMoveTime { get; init; }
```

Duration in seconds of the animated cursor movement as the selection moves from one item to another.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Shadow

```csharp
public Color Shadow { get; init; }
```

Drop-shadow color applied beneath menu item text. Defaults to `Color.Black`.

**Returns** \
[Color](../../Murder/Core/Graphics/Color.html) \

⚡

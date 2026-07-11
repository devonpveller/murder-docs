# DrawMenuStyle

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public sealed struct DrawMenuStyle
```

Holds visual style parameters for drawing a vertical menu via `RenderServices.DrawVerticalMenu`.

**Intent:** Bundles font, color, alignment, animation, and spacing settings for rendered menus.

**Use-case:** Create and configure a `DrawMenuStyle` instance, then pass it to `RenderServices.DrawVerticalMenu` to control how a list of `MenuOption` items is rendered in a UI batch.

### ⭐ Constructors
```csharp
public DrawMenuStyle()
```

### ⭐ Properties
#### Color
```csharp
public Color Color;
```
Color used to render unselected menu items.

**Returns** \
[Color](../../Murder/Core/Graphics/Color.html) \
#### Ease
```csharp
public EaseKind Ease;
```
Easing function applied to the selection cursor movement animation.

**Returns** \
[EaseKind](../../Murder/Utilities/EaseKind.html) \
#### ExtraVerticalSpace
```csharp
public int ExtraVerticalSpace;
```
Additional pixel spacing inserted between each menu item.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Font
```csharp
public int Font;
```
Index of the font used to draw menu item text.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Origin
```csharp
public Vector2 Origin;
```
Normalised origin point (pivot) for the menu layout, e.g. `(0.5, 0)` centres horizontally at the top.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
#### SelectedColor
```csharp
public Color SelectedColor;
```
Color used to render the currently selected menu item.

**Returns** \
[Color](../../Murder/Core/Graphics/Color.html) \
#### SelectorMoveTime
```csharp
public float SelectorMoveTime;
```
Duration in seconds of the animated cursor movement between menu items.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### Shadow
```csharp
public Color Shadow;
```
Drop-shadow color applied beneath menu item text.

**Returns** \
[Color](../../Murder/Core/Graphics/Color.html) \
### ⭐ Methods
#### WithOrigin(Vector2)
```csharp
public DrawMenuStyle WithOrigin(Vector2 origin)
```
Returns a copy of this style with `Origin` set to `origin`.

**Parameters** \
`origin` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[DrawMenuStyle](../../Murder/Services/DrawMenuStyle.html) \



⚡
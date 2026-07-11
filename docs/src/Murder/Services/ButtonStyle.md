# ButtonStyle

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public sealed struct ButtonStyle
```

Defines the visual appearance of an interactive button drawn by the UI system.

**Intent:** Bundles all style parameters (sprite, colors, font, padding) needed to render a styled button.

**Use-case:** Pass to `MurderUiServices` draw methods to control how a menu button looks, including its background sprite, text font and color, outline, shadow, and horizontal padding.

### ⭐ Constructors
```csharp
public ButtonStyle()
```

### ⭐ Properties
#### ExtraPaddingX
```csharp
public Point ExtraPaddingX { get; public set; }
```
Extra horizontal padding added on both sides of the button content area.

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \
#### Font
```csharp
public readonly int Font;
```
Index of the font used for the button label.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### OutlineColor
```csharp
public readonly T? OutlineColor;
```
Optional color for the button border outline; `null` means no outline is drawn.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
#### Sprite
```csharp
public readonly Portrait Sprite;
```
The portrait (sprite and animation) used as the button background.

**Returns** \
[Portrait](../../Murder/Core/Portrait.html) \
#### TextAlignment
```csharp
public readonly float TextAlignment;
```
Horizontal alignment of the button label text in the range [0, 1], where 0 is left-aligned and 1 is right-aligned.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### TextColor
```csharp
public readonly Color TextColor;
```
Color of the button label text.

**Returns** \
[Color](../../Murder/Core/Graphics/Color.html) \
#### TextOutlineColor
```csharp
public readonly T? TextOutlineColor;
```
Optional color for the text outline stroke; `null` means no text outline.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
#### TextShadowColor
```csharp
public readonly T? TextShadowColor;
```
Optional color for the drop shadow beneath the button label; `null` means no shadow.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \


⚡
# DrawMenuInfo

**Namespace:** Murder.Services.Info \
**Assembly:** Murder.dll

```csharp
public sealed struct DrawMenuInfo
```

Return value produced by `RenderServices.DrawVerticalMenu` after it lays out and draws a vertical list of `MenuOption` entries.

**Intent:** Hands back the layout numbers the draw pass just computed (selector position, its previous and eased positions, the widest option's pixel width, the line height, and the final origin used) so the caller can draw extra decoration — such as a selection arrow, a highlight box, or an icon — aligned with the menu without redoing the layout math itself.

**Use-case:** Don't construct this by hand; call `RenderServices.DrawVerticalMenu` and keep the returned `DrawMenuInfo`. Use `SelectorEasedPosition` to draw an animated cursor next to the current selection, and call `GetOptionPosition(index)` to find where any other option in the list was drawn (for example to attach a tooltip or icon to a specific row).

### ⭐ Constructors

```csharp
public DrawMenuInfo()
```

Creates a `DrawMenuInfo` with every field zeroed. Game code does not normally call this directly; `RenderServices.DrawVerticalMenu` builds and returns a populated instance after drawing the menu.

### ⭐ Methods

#### GetOptionPosition(int)

```csharp
public Vector2 GetOptionPosition(int index)
```

Computes the draw position of the menu option at `index`, using this instance's `LineHeight` and `FinalPosition`. This lets a caller find the on-screen position of any row in the menu (not just the currently selected one) after the menu has been drawn, e.g. to anchor an icon or overlay to a specific option.

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

### ⭐ Properties

#### FinalPosition

```csharp
public Point FinalPosition { get; }
```

The clamped top-left origin the menu was actually drawn at (the requested position with negative coordinates clamped to zero). Used by `GetOptionPosition` to compute the position of individual rows.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### LineHeight

```csharp
public int LineHeight { get; }
```

The pixel height of one menu row (the font's line height plus `DrawMenuStyle.ExtraVerticalSpace`), used together with `FinalPosition` to locate individual options via `GetOptionPosition`.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### MaximumSelectionWidth

```csharp
public int MaximumSelectionWidth { get; }
```

The pixel width of the widest option label that was drawn, useful for sizing a selector box or background panel so it comfortably fits every entry in the menu.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### PreviousSelectorPosition

```csharp
public Vector2 PreviousSelectorPosition { get; }
```

Where the selector cursor was anchored before the current selection change, used as the animation start point when easing the cursor toward `SelectorPosition`.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### SelectorEasedPosition

```csharp
public Vector2 SelectorEasedPosition { get; }
```

The selector cursor's actual draw position for this frame, eased between `PreviousSelectorPosition` and `SelectorPosition` according to `DrawMenuStyle.SelectorMoveTime` and `DrawMenuStyle.Ease`. This is normally the value you want when drawing a selection indicator, since it already accounts for the move animation.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### SelectorPosition

```csharp
public Vector2 SelectorPosition { get; }
```

The un-eased target position of the selector cursor for the currently selected option, i.e. where the cursor animation is heading toward this frame.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

⚡

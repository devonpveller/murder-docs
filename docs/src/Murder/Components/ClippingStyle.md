# ClippingStyle

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
sealed enum ClippingStyle : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Determines how the `SpriteClippingRectComponent` reveals or hides portions of a sprite.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

**Intent:** Selects the algorithm used to compute the clipping rectangle so designers can choose between a center-anchored reveal and a border-inset trim.

**Use-case:** Set on `SpriteClippingRectComponent` to control how a health bar, progress fill, or dialogue box iris-wipes open.

### ⭐ Properties

#### CutFromBorders

```csharp
public static const ClippingStyle CutFromBorders;
```

Insets the clipping rectangle from each edge of the sprite by the specified left/right/top/down pixel amounts.

**Returns** \
[ClippingStyle](../../Murder/Components/ClippingStyle.html) \

#### GrowFromCenter

```csharp
public static const ClippingStyle GrowFromCenter;
```

Expands the clipping rectangle outward from the sprite's origin point; a value of `-1` extends to the full border.

**Returns** \
[ClippingStyle](../../Murder/Components/ClippingStyle.html) \

⚡

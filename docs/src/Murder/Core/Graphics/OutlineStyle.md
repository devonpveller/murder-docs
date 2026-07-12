# OutlineStyle

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed enum OutlineStyle : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

Flags controlling which sides of a sprite receive an outline when drawn with `DrawInfo.Outline`.

**Intent:** Enables per-side outline rendering on sprites; combine flags to draw individual edge outlines or all four sides at once.

**Use-case:** Set `DrawInfo.OutlineStyle` to `Full` for a standard selection highlight, or restrict it to `Bottom` or `Top` for stylised drop-shadow effects.

### ⭐ Properties

#### Bottom

```csharp
public static const OutlineStyle Bottom;
```

Draws an outline only on the bottom edge of the sprite.

**Returns** \
[OutlineStyle](../../../Murder/Core/Graphics/OutlineStyle.html) \

#### Full

```csharp
public static const OutlineStyle Full;
```

Draws outlines on all four sides of the sprite (combination of `Top | Right | Bottom | Left`).

**Returns** \
[OutlineStyle](../../../Murder/Core/Graphics/OutlineStyle.html) \

#### Left

```csharp
public static const OutlineStyle Left;
```

Draws an outline only on the left edge of the sprite.

**Returns** \
[OutlineStyle](../../../Murder/Core/Graphics/OutlineStyle.html) \

#### None

```csharp
public static const OutlineStyle None;
```

No outline is drawn regardless of `DrawInfo.Outline` color.

**Returns** \
[OutlineStyle](../../../Murder/Core/Graphics/OutlineStyle.html) \

#### Right

```csharp
public static const OutlineStyle Right;
```

Draws an outline only on the right edge of the sprite.

**Returns** \
[OutlineStyle](../../../Murder/Core/Graphics/OutlineStyle.html) \

#### Top

```csharp
public static const OutlineStyle Top;
```

Draws an outline only on the top edge of the sprite.

**Returns** \
[OutlineStyle](../../../Murder/Core/Graphics/OutlineStyle.html) \

⚡

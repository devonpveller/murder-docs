# ImageFlip

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed enum ImageFlip : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Specifies whether a sprite should be mirrored horizontally, vertically, both, or not at all when drawn.

**Intent:** Provides a clean flag enum for sprite mirroring so draw calls can express flipping without separate boolean parameters.

**Use-case:** Set `DrawInfo.ImageFlip` or pass directly to `AtlasCoordinates.Draw` to flip a sprite; commonly used to face a character left or right without needing separate left-facing art.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### Both

```csharp
public static const ImageFlip Both;
```

Mirrors the sprite both horizontally and vertically (equivalent to a 180° rotation about the center).

**Returns** \
[ImageFlip](../../../Murder/Core/Graphics/ImageFlip.html) \

#### Horizontal

```csharp
public static const ImageFlip Horizontal;
```

Mirrors the sprite left-to-right along the vertical axis.

**Returns** \
[ImageFlip](../../../Murder/Core/Graphics/ImageFlip.html) \

#### None

```csharp
public static const ImageFlip None;
```

No mirroring; draws the sprite as authored.

**Returns** \
[ImageFlip](../../../Murder/Core/Graphics/ImageFlip.html) \

#### Vertical

```csharp
public static const ImageFlip Vertical;
```

Mirrors the sprite top-to-bottom along the horizontal axis.

**Returns** \
[ImageFlip](../../../Murder/Core/Graphics/ImageFlip.html) \

⚡

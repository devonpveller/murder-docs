# ImageFlipServices

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public static class ImageFlipServices
```

Extension helpers for toggling individual axes of an `ImageFlip` flag without having to manually combine or clear the `Horizontal`/`Vertical` bits.

**Intent:** Provides a safe, readable way to flip a sprite along a single axis while preserving whatever flip state already exists on the other axis, since `ImageFlip` is a `[Flags]` enum and naive bitwise toggling is easy to get wrong (e.g. accidentally clearing the vertical flip when only the horizontal one should change).

**Use-case:** Call `imageFlip.FlipHorizontal()` when a character changes facing direction, or `imageFlip.FlipVertical()` for effects like mirrored reflections, without needing to reason about the underlying flag combination.

### ⭐ Methods

#### FlipHorizontal(ImageFlip)

```csharp
public ImageFlip FlipHorizontal(ImageFlip flip)
```

Returns a copy of `flip` with the horizontal flip bit toggled, preserving the vertical bit.

**Parameters** \
`flip` [ImageFlip](../../../Murder/Core/Graphics/ImageFlip.html) \

**Returns** \
[ImageFlip](../../../Murder/Core/Graphics/ImageFlip.html) \

#### FlipVertical(ImageFlip)

```csharp
public ImageFlip FlipVertical(ImageFlip flip)
```

Returns a copy of `flip` with the vertical flip bit toggled, preserving the horizontal bit.

**Parameters** \
`flip` [ImageFlip](../../../Murder/Core/Graphics/ImageFlip.html) \

**Returns** \
[ImageFlip](../../../Murder/Core/Graphics/ImageFlip.html) \

⚡

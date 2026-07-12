# ThreeSliceInfo

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public readonly struct ThreeSliceInfo
```

Serializable definition of a "three-slice" (a nine-slice restricted to one axis) sprite: it stores only the sprite's `Image` GUID and the `Core` rectangle, and is meant to live on components/assets authored in the editor.

**Intent:** Provides the data required to configure a scalable bordered sprite; the GUID is resolved to a [ThreeSlice](../../Murder/Utilities/ThreeSlice.html) struct (with the actual `SpriteAsset` loaded) at runtime.

**Use-case:** Assign to components that need scalable bordered sprites (e.g., dialogue boxes, health bars); resolved into a `ThreeSlice` by the rendering code (`SpriteThreeSliceRenderSystem`).

### ⭐ Constructors

```csharp
public ThreeSliceInfo()
```

Creates an empty `ThreeSliceInfo` with no image and an empty core rectangle. Equivalent to `Empty`.

```csharp
public ThreeSliceInfo(Rectangle core, Guid image)
```

Creates a `ThreeSliceInfo` referencing sprite `image`, stretching the `core` region.

**Parameters** \
`core` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`image` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

### ⭐ Properties

#### Core

```csharp
public readonly Rectangle Core;
```

The sub-rectangle of the sprite (in sprite pixel space) that gets stretched to fill the middle of the drawn area; see `ThreeSlice.Core`.

**Returns** \
[Rectangle](../../Murder/Core/Geometry/Rectangle.html) \

#### Empty

```csharp
public static ThreeSliceInfo Empty { get; }
```

A reusable default value with no image assigned; used as the default for optional three-slice fields on components.

**Returns** \
[ThreeSliceInfo](../../Murder/Utilities/ThreeSliceInfo.html) \

#### Image

```csharp
public readonly Guid Image;
```

GUID of the `SpriteAsset` to draw. Resolved to an actual asset when converted to a `ThreeSlice`.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

⚡

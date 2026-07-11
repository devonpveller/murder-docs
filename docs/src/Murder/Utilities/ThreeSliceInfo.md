# ThreeSliceInfo

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public sealed struct ThreeSliceInfo
```

A serializable definition of a three-slice sprite that stores the core rectangle and the Aseprite sprite asset GUID.

**Intent:** Provides the data required to configure a scalable bordered sprite; the GUID is resolved to a `ThreeSlice` struct at runtime.

**Use-case:** Assign to components that need scalable bordered sprites (e.g., dialogue boxes, health bars); resolved into a `ThreeSlice` by the rendering code.

### ⭐ Constructors
```csharp
public ThreeSliceInfo()
```

Creates an empty `ThreeSliceInfo` with no image and an empty core rectangle.

```csharp
public ThreeSliceInfo(Rectangle core, Guid image)
```

Creates a `ThreeSliceInfo` with the given core region and sprite asset GUID.

**Parameters** \
`core` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`image` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

### ⭐ Properties
#### Core
```csharp
public readonly Rectangle Core;
```

The rectangle within the sprite that is tiled or stretched (the middle section).

**Returns** \
[Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
#### Empty
```csharp
public static ThreeSliceInfo Empty { get; }
```

Returns a default `ThreeSliceInfo` with no image and an empty core rectangle.

**Returns** \
[ThreeSliceInfo](../../Murder/Utilities/ThreeSliceInfo.html) \
#### Image
```csharp
public readonly Guid Image;
```

The GUID of the `SpriteAsset` to use when rendering this three-slice.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \


⚡
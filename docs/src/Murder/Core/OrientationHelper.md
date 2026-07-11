# OrientationHelper

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public static class OrientationHelper
```

Static helper methods for working with `Orientation` values and 2D movement vectors.

**Intent:** Utility class that extracts or determines the dominant orientation from a `Vector2`.

**Use-case:** Call `GetDominantOrientation` to snap an agent's movement vector to its primary axis, or `GetOrientationAmount` to read the component of a vector along a specific axis.

### ⭐ Methods
#### GetOrientationAmount(Vector2, Orientation)
```csharp
public float GetOrientationAmount(Vector2 vector, Orientation orientation)
```

Returns the component of `vector` along the given `orientation` axis (X for Horizontal, Y for Vertical).

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`orientation` [Orientation](../../Murder/Core/Orientation.html) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### GetDominantOrientation(Vector2)
```csharp
public Orientation GetDominantOrientation(Vector2 vector)
```

Returns the `Orientation` of the axis with the greater absolute component in `vector`.

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Orientation](../../Murder/Core/Orientation.html) \



⚡
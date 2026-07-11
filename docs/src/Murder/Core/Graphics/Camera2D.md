# Camera2D

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public class Camera2D
```

Creates a camera 2D world view for our game.

**Intent:** Manages the world-to-screen transform for 2D rendering, including position, zoom, rotation, and screen-shake.

**Use-case:** Access the camera through `RenderContext.Camera`; set `Position` and `Zoom` to control what the player sees, call `Shake()` for screen-shake effects, and use `WorldToScreenPosition()` / `ScreenToWorldPosition()` for coordinate conversions.

### ⭐ Constructors
```csharp
public Camera2D(int width, int height)
```

Creates a camera with the given viewport resolution.

**Parameters** \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`height` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties
#### Aspect
```csharp
public float Aspect { get; }
```

Width-to-height aspect ratio of the camera viewport (`Width / Height`).

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### Bounds
```csharp
public Rectangle Bounds { get; private set; }
```

The axis-aligned world-space rectangle currently visible through the camera, useful for frustum culling.

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \
#### HalfWidth
```csharp
public int HalfWidth { get; }
```

Half the viewport width in pixels; useful when centering objects or computing screen offsets.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Height
```csharp
public int Height { get; private set; }
```

Viewport height in pixels.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Position
```csharp
public Vector2 Position { get; public set; }
```

The top-left world-space position of the camera. Setting this moves the viewport within the game world.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
#### SafeBounds
```csharp
public Rectangle SafeBounds { get; private set; }
```

A slightly inset version of `Bounds` used for safe-area checks (e.g., ensuring spawned entities don't appear right at the viewport edge).

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \
#### ShakeIntensity
```csharp
public float ShakeIntensity;
```

The current pixel magnitude of the screen-shake displacement.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### ShakeTime
```csharp
public float ShakeTime;
```

Remaining duration of the active screen-shake in seconds.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### Size
```csharp
public Point Size { get; }
```

Viewport dimensions as a `Point` (`Width`, `Height`).

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \
#### Width
```csharp
public int Width { get; private set; }
```

Viewport width in pixels.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### WorldViewProjection
```csharp
public Matrix WorldViewProjection { get; }
```

The combined world-view-projection matrix passed to shaders; cached and recomputed only when `Position`, `Zoom`, or rotation changes.

**Returns** \
[Matrix](https://docs.monogame.net/api/Microsoft.Xna.Framework.Matrix.html) \
#### Zoom
```csharp
public float Zoom { get; public set; }
```

Camera zoom factor (1.0 = no zoom). Clamped to [0.1, 500]. Values greater than 1 zoom in; values less than 1 zoom out.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
### ⭐ Methods
#### GetCursorWorldPosition(Point, Point)
```csharp
public Point GetCursorWorldPosition(Point screenOffset, Point viewportSize)
```

Get coordinates of the cursor in the world.
            Ideally you should use the EditorHook for this if you are in an editor System.

**Parameters** \
`screenOffset` [Point](../../../Murder/Core/Geometry/Point.html) \
`viewportSize` [Point](../../../Murder/Core/Geometry/Point.html) \

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### ConvertWorldToScreenPosition(Vector2, Point)
```csharp
public Vector2 ConvertWorldToScreenPosition(Vector2 position, Point viewportSize)
```

Get coordinates of the cursor in the world.

**Parameters** \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`viewportSize` [Point](../../../Murder/Core/Geometry/Point.html) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### ScreenToWorldPosition(Vector2)
```csharp
public Vector2 ScreenToWorldPosition(Vector2 screenPosition)
```

Converts a screen-space position to world-space coordinates using the current camera transform.

**Parameters** \
`screenPosition` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### WorldToScreenPosition(Vector2)
```csharp
public Vector2 WorldToScreenPosition(Vector2 screenPosition)
```

Converts a world-space position to screen-space coordinates using the current camera transform.

**Parameters** \
`screenPosition` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### ClearCache()
```csharp
public void ClearCache()
```

Forces the cached `WorldViewProjection` matrix to be recomputed on next access, typically after the viewport resolution changes.

#### Lock()
```csharp
public void Lock()
```

Prevents further changes to `Position` from updating the camera transform until `Unlock()` is called; useful during cinematic sequences.

#### Rotate(float)
```csharp
public void Rotate(float degrees)
```

Rotates the camera by `degrees` (added to the current rotation). Invalidates the cached transform.

**Parameters** \
`degrees` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Shake(float, float)
```csharp
public void Shake(float intensity, float time)
```

Triggers a screen-shake effect with the given pixel `intensity` that decays over `time` seconds.

**Parameters** \
`intensity` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`time` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Unlock()
```csharp
public void Unlock()
```

Re-enables position updates after a `Lock()` call.



⚡
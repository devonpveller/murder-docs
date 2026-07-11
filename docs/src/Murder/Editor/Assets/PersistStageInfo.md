# PersistStageInfo

**Namespace:** Murder.Editor.Assets \
**Assembly:** Murder.dll

```csharp
public sealed struct PersistStageInfo
```

Stores the last-known camera state for an editor stage so it can be restored on next open.

**Intent:** Persists the editor camera's position, viewport size, and zoom level per-stage so the developer returns to the same view after reopening a scene.

**Use-case:** Saved automatically by the editor into `EditorSettingsAsset.CameraPositions` whenever the user navigates the stage view.

### ⭐ Constructors
```csharp
public PersistStageInfo(Point position, Point size, int zoom)
```
Creates a snapshot of the current camera position, viewport size, and zoom level.

**Parameters** \
`position` [Point](../../../Murder/Core/Geometry/Point.html) \
`size` [Point](../../../Murder/Core/Geometry/Point.html) \
`zoom` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties
#### Position
```csharp
public readonly Point Position;
```
World-space pixel position of the camera when this snapshot was taken.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \
#### Size
```csharp
public readonly Point Size;
```

Size of the camera when this was saved.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \
#### Zoom
```csharp
public readonly int Zoom;
```
Zoom level of the editor camera when this snapshot was taken.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \


⚡
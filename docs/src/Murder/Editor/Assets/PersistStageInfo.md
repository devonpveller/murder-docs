# PersistStageInfo

**Namespace:** Murder.Editor.Assets \
**Assembly:** Murder.dll

```csharp
public readonly struct PersistStageInfo
```

Immutable snapshot of an editor stage's camera and overlay state, taken whenever the developer navigates a stage view.

**Intent:** Stored in [EditorSettingsAsset.StageInfo](../../../Murder/Editor/Assets/EditorSettingsAsset.html#stageinfo) keyed by the stage/asset GUID so the editor can restore the exact same camera position, viewport size, zoom level and debug overlay flags the next time that asset is opened, instead of resetting to a default view every time.

**Use-case:** Written by the editor's stage view every time the camera moves or is resized, and read back by `AssetEditor`/`Stage` when an asset is opened, to reposition the camera and toggle the same debug overlays ([StageSetting](../../../Murder/Editor/Assets/StageSetting.html)) the developer last had enabled.

### ⭐ Constructors

```csharp
public PersistStageInfo(Point position, Point size, int zoom, StageSetting settings)
```

Creates a snapshot of the current camera position, viewport size, zoom level and debug overlay flags.

**Parameters** \
`position` [Point](../../../Murder/Core/Geometry/Point.html) -- world-space pixel position of the camera. \
`size` [Point](../../../Murder/Core/Geometry/Point.html) -- viewport size of the camera. \
`zoom` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) -- zoom level of the editor camera. \
`settings` [StageSetting](../../../Murder/Editor/Assets/StageSetting.html) -- debug overlay flags currently enabled for the stage. \

### ⭐ Properties

#### Position

```csharp
public readonly Point Position;
```

World-space pixel position of the camera when this snapshot was taken.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### Settings

```csharp
public readonly StageSetting Settings;
```

Which debug overlays ([StageSetting](../../../Murder/Editor/Assets/StageSetting.html)) were enabled when this snapshot was taken -- e.g. whether collider, sprite or sound gizmos were being drawn. Defaults to `StageSetting.ShowCollider`.

**Returns** \
[StageSetting](../../../Murder/Editor/Assets/StageSetting.html) \

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

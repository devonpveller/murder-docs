# FacingInfo

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct FacingInfo
```

Describes one directional slice of a sprite's facing configuration, mapping an angular range to an animation suffix and optional flip flag.

**Intent:** Stores the data for a single facing slice in `SpriteFacingComponent` so the sprite system can select the correct directional animation and whether to mirror it.

**Use-case:** Populated in the `SpriteFacingComponent.FacingInfo` array by the editor; each entry covers an arc of `AngleSize` radians and contributes a suffix (e.g., `"_right"`) and optional horizontal flip to the animation name lookup.

### ⭐ Properties
#### AngleSize
```csharp
public float AngleSize { get; public set; }
```

The arc width (in radians) that this facing slice covers.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### Flip
```csharp
public bool Flip { get; public set; }
```

When `true`, the sprite should be horizontally flipped for this facing direction.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Suffix
```csharp
public string Suffix { get; public set; }
```

Animation name suffix appended when this facing slice is active (e.g., `"_right"`, `"_up"`).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \


⚡
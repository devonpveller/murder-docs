# FacingInfo

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct FacingInfo
```

Describes one directional slice of a sprite's facing configuration, mapping an angular range to an animation suffix and optional flip flag.

**Intent:** Stores the data for a single facing slice in [SpriteFacingComponent](../../Murder/Components/SpriteFacingComponent.html) so `SpriteFacingComponent.GetSuffixFromAngle` can walk the ordered list of slices, accumulate their `AngleSize`, and pick the first slice whose accumulated angle covers the queried facing angle.

**Use-case:** Populated in the `SpriteFacingComponent.FacingInfo` array (typically authored/resized via the editor and `SpriteFacingComponent.Resize`); each entry covers an arc of `AngleSize` radians starting where the previous slice left off, and contributes a `Suffix` (e.g., `"_right"`) and optional horizontal `Flip` to the animation name lookup used to pick the correctly-facing sprite animation.

### ⭐ Properties

#### AngleSize

```csharp
public readonly float AngleSize { get; init; }
```

The arc width (in radians) that this facing slice covers, measured cumulatively from the facing component's `AngleStart`.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Flip

```csharp
public readonly bool Flip { get; init; }
```

When `true`, the sprite should be horizontally flipped for this facing direction.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Suffix

```csharp
public readonly string Suffix { get; init; }
```

Animation name suffix appended when this facing slice is active (e.g., `"_right"`, `"_up"`).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

⚡

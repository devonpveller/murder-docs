# SpriteFacingComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct SpriteFacingComponent : IComponent
```

Controls how a sprite's animation suffix and horizontal flip change based on the entity's movement or facing angle. Each `FacingInfo` entry maps an angular slice to a suffix string and optional flip.

**Intent:** Drive directional animation selection (e.g. "\_up", "\_down", "\_side") and flipping automatically from the entity's angle.

**Use-case:** Attach to a character entity alongside a directional movement component; `DirectionHelper.GetSuffixFromAngle(entity, prefix, angle)` reads it (falling back from an `OverrideSpriteFacingComponent` entry, if present) and calls `GetSuffixFromAngle` to resolve which animation suffix (e.g. `"_n"`, `"_se"`) and horizontal-flip flag the sprite should use for the entity's current facing angle. Editor tooling (`SpriteFacingComponentEditor`, `SpriteRenderDebugSystem`) uses `Resize` to grow or shrink the number of `FacingInfo` slices while an artist configures the directional slices in the editor.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public SpriteFacingComponent()
```

### ⭐ Properties

#### AngleStart

```csharp
public readonly float AngleStart { get; init; }
```

Starting angle offset (in radians) applied before slicing into facing segments.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### DefaultFlip

```csharp
public bool DefaultFlip { get; init; }
```

Default horizontal flip state used when no facing segment overrides it.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### DefaultSuffix

```csharp
public readonly string DefaultSuffix { get; init; }
```

Animation suffix appended to the base animation name when no facing-info entry matches.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### FacingInfo

```csharp
public readonly ImmutableArray<T> FacingInfo { get; init; }
```

Ordered list of [FacingInfo](../../Murder/Components/FacingInfo.html) slices, each specifying an angular width, a suffix, and a flip state for that directional segment. `GetSuffixFromAngle` walks this list in order, accumulating each slice's `AngleSize`, to find the slice covering a given angle.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

### ⭐ Methods

#### Resize(int, int)

```csharp
public SpriteFacingComponent Resize(int atIndex, int slices)
```

Returns a new component with its [FacingInfo](../../Murder/Components/FacingInfo.html) array resized to `slices` entries: trims items (starting near `atIndex`) if `slices` is smaller than the current length, and inserts default `FacingInfo` entries (with a small `AngleSize` of `0.1f`) if `slices` is larger. Used by the editor to grow/shrink the number of directional slices while authoring a facing configuration.

**Parameters** \
`atIndex` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`slices` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[SpriteFacingComponent](../../Murder/Components/SpriteFacingComponent.html) \

#### GetSuffixFromAngle(float)

```csharp
public ValueTuple<T1, T2> GetSuffixFromAngle(float angle)
```

Normalizes `angle` relative to `AngleStart` and walks `FacingInfo` accumulating each slice's `AngleSize` until it finds the slice covering the angle, returning its `Suffix` and `Flip`. Falls back to `(DefaultSuffix, DefaultFlip)` if no slice matches.

**Parameters** \
`angle` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[ValueTuple\<T1, T2\>](https://learn.microsoft.com/en-us/dotnet/api/System.ValueTuple-2?view=net-7.0) \

⚡

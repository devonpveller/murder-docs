# SpriteFacingComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct SpriteFacingComponent : IComponent
```

Controls how a sprite's animation suffix and horizontal flip change based on the entity's movement or facing angle. Each `FacingInfo` entry maps an angular slice to a suffix string and optional flip.

**Intent:** Drive directional animation selection (e.g. "_up", "_down", "_side") and flipping automatically from the entity's angle.

**Use-case:** Attach to a character entity alongside a directional movement component; as the character's angle changes, this component selects the correct animation suffix and flip state.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public SpriteFacingComponent()
```

### ⭐ Properties
#### AngleStart
```csharp
public float AngleStart { get; public set; }
```

Starting angle offset (in radians) applied before slicing into facing segments.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### DefaultFlip
```csharp
public bool DefaultFlip { get; public set; }
```

Default horizontal flip state used when no facing segment overrides it.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### DefaultSuffix
```csharp
public string DefaultSuffix { get; public set; }
```

Animation suffix appended to the base animation name when no facing-info entry matches.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### FacingInfo
```csharp
public ImmutableArray<T> FacingInfo { get; public set; }
```

Ordered list of angular slices, each specifying a suffix and flip state for that directional segment.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
### ⭐ Methods
#### Resize(int, int)
```csharp
public SpriteFacingComponent Resize(int atIndex, int slices)
```

Returns a new [Murder.Components.SpriteFacingComponent.FacingInfo]() resized.
            Trims the last items if 'slices' is smaller than current length, and adds default values if larger.

**Parameters** \
`atIndex` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`slices` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[SpriteFacingComponent](../../Murder/Components/SpriteFacingComponent.html) \

#### GetSuffixFromAngle(float)
```csharp
public ValueTuple<T1, T2> GetSuffixFromAngle(float angle)
```

Gets the suffix and flip state based on a specified angle.

**Parameters** \
`angle` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
\

**Returns** \
[ValueTuple\<T1, T2\>](https://learn.microsoft.com/en-us/dotnet/api/System.ValueTuple-2?view=net-7.0) \
\



⚡
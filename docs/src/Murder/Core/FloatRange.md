# FloatRange

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public sealed struct FloatRange
```

Range of float values.

**Intent:** A min–max pair of floats used to represent a continuous range.

**Use-case:** Pass a `FloatRange` to particle emitters, randomized spawn offsets, or any system that needs to draw a random value or interpolate between two bounds.

### ⭐ Constructors
```csharp
public FloatRange(float start, float end)
```

Creates a float range with the given inclusive lower and upper bounds.

**Parameters** \
`start` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`end` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties
#### End
```csharp
public readonly float End;
```

The inclusive upper bound of the range.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### Start
```csharp
public readonly float Start;
```

The inclusive lower bound of the range.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
### ⭐ Methods
#### Contains(float)
```csharp
public bool Contains(float v)
```

Returns `true` when `v` falls within `[Start, End]` (inclusive).

**Parameters** \
`v` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### GetRandom()
```csharp
public float GetRandom()
```

Returns a uniformly distributed random float within this range using the shared `Game.Random` instance.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### GetRandom(Random)
```csharp
public float GetRandom(Random random)
```

Returns a uniformly distributed random float within this range using the supplied `random` source.

**Parameters** \
`random` [Random](https://learn.microsoft.com/en-us/dotnet/api/System.Random?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Lerp(float)
```csharp
public float Lerp(float progress)
```

Linearly interpolates from `Start` to `End` by `progress` (0 = Start, 1 = End).

**Parameters** \
`progress` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \



⚡
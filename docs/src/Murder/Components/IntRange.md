# IntRange

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct IntRange
```

Represents an inclusive integer interval with a start and end value, used for random number generation and range checks.

**Intent:** Provide a compact, serializable min/max integer range suitable for editor-configurable parameters like spawn counts or damage values.

**Use-case:** Declare as a field on a component and set `Start`/`End` in the editor; call `GetRandom()` to draw a random integer within the range, or `Contains()` to test membership.

### ⭐ Constructors
```csharp
public IntRange(int single)
```

**Parameters** \
`single` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

```csharp
public IntRange(int start, int end)
```

**Parameters** \
`start` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`end` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties
#### End
```csharp
public readonly int End;
```

Inclusive upper bound of the range.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Start
```csharp
public readonly int Start;
```

Inclusive lower bound of the range.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Zero
```csharp
public readonly static IntRange Zero;
```

A pre-defined range where both `Start` and `End` are 0.

**Returns** \
[IntRange](../../Murder/Components/IntRange.html) \
### ⭐ Methods
#### Contains(float)
```csharp
public bool Contains(float v)
```

Returns `true` if `v` falls within `[Start, End]` inclusive.

**Parameters** \
`v` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Contains(int)
```csharp
public bool Contains(int v)
```

Returns `true` if `v` falls within `[Start, End]` inclusive.

**Parameters** \
`v` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Get(float)
```csharp
public float Get(float progress)
```

Linearly interpolates between `Start` and `End` by `progress` (0 = Start, 1 = End).

**Parameters** \
`progress` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### GetRandom()
```csharp
public float GetRandom()
```

Returns a random integer value within `[Start, End)` using the shared game random instance.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### GetRandomFloat(Random)
```csharp
public float GetRandomFloat(Random random)
```

Returns a random float value within `[Start, End)` using the provided `Random` instance.

**Parameters** \
`random` [Random](https://learn.microsoft.com/en-us/dotnet/api/System.Random?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### GetRandom(Random)
```csharp
public int GetRandom(Random random)
```

Returns a random integer value within `[Start, End)` using the provided `Random` instance.

**Parameters** \
`random` [Random](https://learn.microsoft.com/en-us/dotnet/api/System.Random?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \



⚡
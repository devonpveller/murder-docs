# AnimationSequence

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct AnimationSequence
```

Defines a candidate follow-up animation clip with a probability weight used for weighted-random selection when the current clip finishes.

**Intent:** Allows an animation to chain into one of several possible next clips instead of a single fixed successor.

**Use-case:** Populate `Animation.NextAnimation` with one or more `AnimationSequence` entries; the runtime picks a successor clip according to their relative `Chance` weights.

### ⭐ Constructors
```csharp
public AnimationSequence(string nextAnimation, float chance)
```

Creates an entry pointing to `nextAnimation` with the given selection `chance` weight.

**Parameters** \
`nextAnimation` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`chance` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties
#### Chance
```csharp
public readonly float Chance;
```

Relative probability weight for selecting this entry during weighted-random successor selection. Higher values increase the chance of being chosen.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### Next
```csharp
public readonly string Next;
```

The name of the animation clip to play next if this entry is selected.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
### ⭐ Methods
#### CreateIfPossible(string)
```csharp
public T? CreateIfPossible(string userData)
```

Parses a comma-separated `userData` string of `clipName:weight` pairs into an `ImmutableArray<AnimationSequence>`. Returns an empty array if `userData` is null or whitespace.

**Parameters** \
`userData` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \



⚡
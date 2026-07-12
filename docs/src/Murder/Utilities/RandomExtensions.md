# RandomExtensions

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public static class RandomExtensions
```

Extension methods on `System.Random` (and a couple of static helpers) that cover the randomization patterns games need constantly: probability gates, coin flips, picking/removing a random element from a collection, random directions, and smoothly-varying "random" curves.

**Intent:** Most gameplay code should call these on `Game.Random` rather than constructing a new `Random`, so results stay deterministic with the rest of the simulation.

**Use-case:** Use `FlipACoin` for 50/50 decisions, `TryWithChanceOf` for probability gates, `NextFloat` for random float values in a range, `GetRandom`/`AnyOf`/`PopRandom` to pick or consume elements from a list/dictionary, and `Direction`/`DistributedDirection` for random or evenly-spread unit vectors.

### ⭐ Methods

#### FlipACoin(Random)

```csharp
public bool FlipACoin(Random random)
```

Returns `true` with 50% probability.

**Parameters** \
`random` [Random](https://learn.microsoft.com/en-us/dotnet/api/System.Random?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TryWithChanceOf(Random, float)

```csharp
public bool TryWithChanceOf(Random random, float chance)
```

Flag a switch with a chance of `chance`, from 0 to 1.

**Parameters** \
`random` [Random](https://learn.microsoft.com/en-us/dotnet/api/System.Random?view=net-7.0) \
`chance` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) — Chance of succeeding, from 0 to 1. \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TryWithChanceOf(Random, int)

```csharp
public bool TryWithChanceOf(Random random, int chance)
```

Flag a switch with a chance of `chance`%.

**Parameters** \
`random` [Random](https://learn.microsoft.com/en-us/dotnet/api/System.Random?view=net-7.0) \
`chance` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) — Chance of succeeding, as a percentage (0-100). \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### SmoothRandom(float, float)

```csharp
public float SmoothRandom(float seed, float smoothness)
```

Samples [PerlinNoise](../../Murder/Utilities/PerlinNoise.html)'s `Noise` along a single axis, producing a smoothly-varying pseudo-random value in `[0, 1]` as `seed` changes, instead of the abrupt jumps a plain `Random` call would give. Used to drive continuous "random" wobble (e.g. glitchy text jitter in `PixelFont`) where nearby seeds should produce nearby results.

**Parameters** \
`seed` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) — Position along the noise curve; small changes produce small changes in the result. \
`smoothness` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) — Scales `seed` before sampling — larger values make the curve vary faster. \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### AnyOf(Random, IList\<T\>)

```csharp
public T AnyOf(Random r, IList<T> arr)
```

Returns a uniformly random element from `arr`. The list is not modified.

**Parameters** \
`r` [Random](https://learn.microsoft.com/en-us/dotnet/api/System.Random?view=net-7.0) \
`arr` [IList\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IList-1?view=net-7.0) \

**Returns** \
[T](../../) \

#### NextFloat(Random)

```csharp
public float NextFloat(Random r)
```

Returns a float from 0f to 1f.

**Parameters** \
`r` [Random](https://learn.microsoft.com/en-us/dotnet/api/System.Random?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### PopRandom(IList\<T\>, Random)

```csharp
public T PopRandom(IList<T> list, Random random)
```

Removes and returns a uniformly random element from `list`. The list shrinks by one.

**Parameters** \
`list` [IList\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IList-1?view=net-7.0) \
`random` [Random](https://learn.microsoft.com/en-us/dotnet/api/System.Random?view=net-7.0) \

**Returns** \
[T](../../) \

#### TryGetRandom(IDictionary\<T, U\>, Random)

```csharp
public U? TryGetRandom(IDictionary<T, U> dict, Random random)
```

Returns the value of a uniformly random entry in `dict`, or `default` if the dictionary is empty. The dictionary is not modified.

**Parameters** \
`dict` [IDictionary\<T, U\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IDictionary-2?view=net-7.0) \
`random` [Random](https://learn.microsoft.com/en-us/dotnet/api/System.Random?view=net-7.0) \

**Returns** \
[U](../../) \

#### TryGetRandomKey(IDictionary\<T, U\>, Random)

```csharp
public T? TryGetRandomKey(IDictionary<T, U> dict, Random random)
```

Returns the key of a uniformly random entry in `dict`, or `default` if the dictionary is empty. The dictionary is not modified.

**Parameters** \
`dict` [IDictionary\<T, U\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IDictionary-2?view=net-7.0) \
`random` [Random](https://learn.microsoft.com/en-us/dotnet/api/System.Random?view=net-7.0) \

**Returns** \
[T](../../) \

#### PopRandom(Dictionary\<T, U\>, Random)

```csharp
public U? PopRandom(Dictionary<T, U> dict, Random random)
```

Removes and returns the value of a uniformly random entry in `dict`, or `default` if the dictionary is empty.

**Parameters** \
`dict` [Dictionary\<T, U\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \
`random` [Random](https://learn.microsoft.com/en-us/dotnet/api/System.Random?view=net-7.0) \

**Returns** \
[U](../../) \

#### GetRandom(IList\<T\>, Random)

```csharp
public T GetRandom(IList<T> array, Random random)
```

Returns a uniformly random element from `array`. The list is not modified.

**Parameters** \
`array` [IList\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IList-1?view=net-7.0) \
`random` [Random](https://learn.microsoft.com/en-us/dotnet/api/System.Random?view=net-7.0) \

**Returns** \
[T](../../) \

#### GetRandom(ImmutableArray\<T\>, Random)

```csharp
public T GetRandom(ImmutableArray<T> array, Random random)
```

Returns a uniformly random element from `array`.

**Parameters** \
`array` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
`random` [Random](https://learn.microsoft.com/en-us/dotnet/api/System.Random?view=net-7.0) \

**Returns** \
[T](../../) \

#### NextFloat(Random, float, float)

```csharp
public float NextFloat(Random r, float min, float max)
```

Returns a random float uniformly distributed in the range `[min, max)`.

**Parameters** \
`r` [Random](https://learn.microsoft.com/en-us/dotnet/api/System.Random?view=net-7.0) \
`min` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`max` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### NextFloat(Random, float)

```csharp
public float NextFloat(Random r, float max)
```

Returns a random float uniformly distributed in the range `[0, max)`.

**Parameters** \
`r` [Random](https://learn.microsoft.com/en-us/dotnet/api/System.Random?view=net-7.0) \
`max` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Direction(Random, float, float)

```csharp
public Vector2 Direction(Random r, float minAngle, float maxAngle)
```

This returns a vector rotated to a random angle from `minAngle` to `maxAngle`.

**Parameters** \
`r` [Random](https://learn.microsoft.com/en-us/dotnet/api/System.Random?view=net-7.0) \
`minAngle` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`maxAngle` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Direction(Random)

```csharp
public Vector2 Direction(Random r)
```

Returns a unit vector pointing in a uniformly random direction (angle from 0 to 2π).

**Parameters** \
`r` [Random](https://learn.microsoft.com/en-us/dotnet/api/System.Random?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### DistributedDirection(Random, int, int, float, float)

```csharp
public Vector2 DistributedDirection(Random r, int currentStep, int totalSteps, float min, float max)
```

Combines `DistributedDirection(Random, int, int)` with a random magnitude in `[min, max)`, giving a vector aimed into the current angular slice with a random length. Useful for spawning particles or projectiles spread evenly in a circle but with varied reach.

**Parameters** \
`r` [Random](https://learn.microsoft.com/en-us/dotnet/api/System.Random?view=net-7.0) \
`currentStep` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`totalSteps` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`min` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`max` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### DistributedDirection(Random, int, int)

```csharp
public Vector2 DistributedDirection(Random r, int currentStep, int totalSteps)
```

Divides a full circle into `totalSteps` equal angular slices and returns a unit vector aimed at a random angle within the `currentStep`-th slice. Used to spread N spawned entities (e.g. particles, burst projectiles) evenly around a circle while still keeping some randomness within each slice, avoiding the visible clumping of pure uniform-random directions.

**Parameters** \
`r` [Random](https://learn.microsoft.com/en-us/dotnet/api/System.Random?view=net-7.0) \
`currentStep` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`totalSteps` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### GetRandom(Random, T[], int)

```csharp
public T[] GetRandom(Random random, T[] array, int length)
```

Get up to `length` random elements in `array`, without repeats. Internally builds an index pool and removes a random index each pick, so no element can be returned twice (unless `length` exceeds `array.Length`, in which case this throws).

**Parameters** \
`random` [Random](https://learn.microsoft.com/en-us/dotnet/api/System.Random?view=net-7.0) \
`array` [T[]](../../) \
`length` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[T[]](../../) \

⚡

# GridNumberExtensions

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public static class GridNumberExtensions
```

Numeric extensions that are grid related.

**Intent:** Extension methods for treating raw `int` values as bit-layer indices and bitmasks, used pervasively by the collision (`CollisionLayersBase`) and tag (`MurderTagsBase`) systems, both of which represent their categories as `int` constants rather than a `[Flags] enum`.

**Use-case:** Call `HasFlag` to test whether a combined collision or tag bitmask (e.g. the value returned by `Map.At`) includes a specific layer, or `ToMask` to convert a zero-based layer index into its bitmask equivalent when defining a new layer constant.

### ⭐ Methods

#### HasFlag(int, int)

```csharp
public bool HasFlag(int value, int mask)
```

Returns `true` when any bit in `mask` is set in `value`. The idiomatic way to test a raw `int` collision/tag bitmask without reaching for `Enum.HasFlag`, which does not apply to plain integers.

**Parameters** \
`value` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`mask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### ToMask(int)

```csharp
public int ToMask(int value)
```

Converts a zero-based layer/bit index to its corresponding power-of-two bitmask (`1 << value`). Used to turn a layer index (e.g. from `CollisionLayersBase`) into the bit that represents it in a combined mask.

**Parameters** \
`value` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡

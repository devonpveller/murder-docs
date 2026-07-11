# GridNumberExtensions

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public static class GridNumberExtensions
```

Numeric extensions that are grid related.

**Intent:** Extension methods for integer values used in grid/bitmask operations.

**Use-case:** Call `HasFlag` to test whether a tile's collision mask includes a specific layer, or `ToMask` to convert a layer index to its bitmask equivalent.

### ⭐ Methods
#### HasFlag(int, int)
```csharp
public bool HasFlag(int value, int mask)
```

Returns `true` when all bits in `mask` are set in `value`.

**Parameters** \
`value` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`mask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### ToMask(int)
```csharp
public int ToMask(int value)
```

Converts a zero-based layer index to its corresponding power-of-two bitmask (`1 << value`).

**Parameters** \
`value` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \



⚡
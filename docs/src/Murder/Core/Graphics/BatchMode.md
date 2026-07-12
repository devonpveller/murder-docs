# BatchMode

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed enum BatchMode : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

How SpriteBatch rendering should behave.

**Intent:** Selects the draw-call ordering and batching strategy for a `Batch2D`, balancing visual correctness (depth order) against GPU efficiency (fewer texture swaps).

**Use-case:** Choose `DepthSortDescending` for painter's-algorithm world sprites, `DrawOrder` for UI layers where submission order already guarantees correct overlap, or `Immediate` for one-off debug draws.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### DepthSortAscending

```csharp
public static const BatchMode DepthSortAscending;
```

Sort batches by Layer Depth using ascending order, but still trying to group as many batches as possible to reduce draw calls.

**Returns** \
[BatchMode](../../../Murder/Core/Graphics/BatchMode.html) \

#### DepthSortDescending

```csharp
public static const BatchMode DepthSortDescending;
```

Sort batches by Layer Depth using descending order, but still trying to group as many batches as possible to reduce draw calls.

**Returns** \
[BatchMode](../../../Murder/Core/Graphics/BatchMode.html) \

#### DrawOrder

```csharp
public static const BatchMode DrawOrder;
```

Standard way. Will respect SpriteBatch.Draw\*() call order, ignoring Layer Depth, but still trying to group as many batches as possible to reduce draw calls.

**Returns** \
[BatchMode](../../../Murder/Core/Graphics/BatchMode.html) \

#### Immediate

```csharp
public static const BatchMode Immediate;
```

Every SpriteBatch.Draw\*() will result in an isolate draw call. No batching will be made, so be careful.

**Returns** \
[BatchMode](../../../Murder/Core/Graphics/BatchMode.html) \

⚡

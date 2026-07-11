# SmartFloat

**Namespace:** Murder.Core.Smart \
**Assembly:** Murder.dll

```csharp
public sealed struct SmartFloat
```

A float value that can either hold a literal constant or reference an index into a `SmartFloatAsset`, allowing game designers to drive values from centralized assets.

**Intent:** Provides a runtime-resolved float that can be authored as a literal or as a reference to a data asset, enabling data-driven tuning without code changes.

**Use-case:** Use on components whose numeric values (speed, damage, range) should be tweakable from a shared asset; the `Float` property always resolves the final value.

### ⭐ Constructors
```csharp
public SmartFloat()
```

Creates a `SmartFloat` with value 0 and no asset reference.

```csharp
public SmartFloat(float custom)
```

Creates a `SmartFloat` that always returns the given literal `custom` value.

**Parameters** \
`custom` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

```csharp
public SmartFloat(Guid guid, int index, float custom)
```

Creates a `SmartFloat` that resolves its value from a `SmartFloatAsset` identified by `guid` and `index`, falling back to `custom` if the asset is unavailable.

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`custom` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties
#### Asset
```csharp
public readonly Guid Asset;
```

The GUID of the `SmartFloatAsset` to resolve the value from, or `Guid.Empty` for a literal value.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### Custom
```csharp
public readonly float Custom;
```

The literal float value used when `Asset` is empty or the asset cannot be resolved.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### Float
```csharp
public float Float { get; }
```

The resolved float value: reads from the referenced `SmartFloatAsset` if available, otherwise returns `Custom`.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### Index
```csharp
public readonly int Index;
```

The index into the `SmartFloatAsset` array to read when resolving the value.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \


⚡
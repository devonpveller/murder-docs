# SmartInt

**Namespace:** Murder.Core.Smart \
**Assembly:** Murder.dll

```csharp
public sealed struct SmartInt
```

An integer value that can hold a literal constant or reference an index into a `SmartIntAsset`, enabling data-driven numeric authoring.

**Intent:** Provides a runtime-resolved integer that designers can drive from a shared asset or override with a literal value.

**Use-case:** Use on components with integer parameters (counts, thresholds, layer indices) that should be shareable across many entities via a central `SmartIntAsset`.

### ⭐ Constructors

```csharp
public SmartInt()
```

Creates a `SmartInt` with value 0 and no asset reference.

```csharp
public SmartInt(Guid guid, int index, int custom)
```

Creates a `SmartInt` that resolves its value from a `SmartIntAsset` identified by `guid` and `index`, falling back to `custom`.

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`custom` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

```csharp
public SmartInt(int custom)
```

Creates a `SmartInt` that always returns the given literal `custom` value.

**Parameters** \
`custom` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties

#### Asset

```csharp
public readonly Guid Asset;
```

The GUID of the `SmartIntAsset` to resolve the value from, or `Guid.Empty` for a literal value.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### Custom

```csharp
public readonly int Custom;
```

The literal integer value used when `Asset` is empty or cannot be resolved.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Index

```csharp
public readonly int Index;
```

The index into the `SmartIntAsset` array to read when resolving the value.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Int

```csharp
public int Int { get; }
```

The resolved integer value: reads from the referenced `SmartIntAsset` if available, otherwise returns `Custom`.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡

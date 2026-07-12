# AssetRef\<T\>

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public sealed struct AssetRef<T>
```

A lightweight, serializable reference to a typed `GameAsset` identified by its GUID; resolves the asset on demand from the game's data store.

**Intent:** Provides a type-safe, GUID-based handle to a `GameAsset` so that asset references can be stored in components and resolved at runtime.

**Use-case:** Store in components or config data wherever you need a reference to a game asset; call `Asset` to get the loaded instance or `TryAsset` for a null-safe lookup.

### ⭐ Constructors

```csharp
public AssetRef<T>(Guid guid)
```

Creates a new `AssetRef<T>` that points to the asset identified by `guid`.

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

### ⭐ Properties

#### Asset

```csharp
public T Asset { get; }
```

Retrieves the asset from the data store by `Guid` via `Game.Data.GetAsset<T>`; throws if `Guid` is empty or the asset does not exist. Use `TryAsset` instead when the reference may not be set.

**Returns** \
[T](../../) \

#### Empty

```csharp
public static AssetRef<T> Empty { get; }
```

Returns an `AssetRef<T>` with an empty `Guid`, representing no asset.

**Returns** \
[AssetRef\<T\>](../../Murder/Utilities/AssetRef-1.html) \

#### Guid

```csharp
public readonly Guid Guid;
```

The unique identifier of the referenced asset; `Guid.Empty` means no asset is referenced.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### HasValue

```csharp
public bool HasValue { get; }
```

Returns `true` if `Guid` is not empty, indicating this reference points to a valid asset.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TryAsset

```csharp
public T? TryAsset { get; }
```

Null-safe counterpart to `Asset`: returns the asset from the data store via `Game.Data.TryGetAsset<T>`, or `null` if `Guid` is empty or the asset cannot be found. Prefer this over `Asset` whenever the reference might legitimately be unset (e.g. an optional component field), since `Asset` throws in that case.

**Returns** \
[T?](../../) \

⚡

# GameAssetIdInfo

**Namespace:** Murder.Attributes \
**Assembly:** Murder.dll

```csharp
public sealed struct GameAssetIdInfo
```

Bundles the target `GameAsset` type and the inheritance flag from a `GameAssetIdAttribute` into a single value object for editor use.

**Intent:** Aggregate the asset-type metadata from `GameAssetIdAttribute` into a convenient struct that editor rendering code can query.

**Use-case:** Typically created internally when the editor reads a `GameAssetIdAttribute` from a field. Pass it to editor systems that need both the allowed asset type and whether derived types are also accepted.

### ⭐ Constructors

```csharp
public GameAssetIdInfo(Type t, bool allowInheritance)
```

Creates a new info record with the specified asset type and inheritance flag.

**Parameters** \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
`allowInheritance` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

### ⭐ Properties

#### AllowInheritance

```csharp
public readonly bool AllowInheritance;
```

Whether it should look for all assets that inherit from this asset.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### AssetType

```csharp
public readonly Type AssetType;
```

The type of the game asset.

**Returns** \
[Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

⚡

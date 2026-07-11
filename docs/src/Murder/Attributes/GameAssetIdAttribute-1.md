# GameAssetIdAttribute\<T\>

**Namespace:** Murder.Attributes \
**Assembly:** Murder.dll

```csharp
public class GameAssetIdAttribute<T> : GameAssetIdAttribute
```

A strongly-typed convenience variant of `GameAssetIdAttribute` that infers the target `GameAsset` subtype from the generic parameter `T`.

**Intent:** Provide a type-safe shorthand for marking `Guid` fields as references to a specific `GameAsset` subtype without passing `typeof(T)` explicitly.

**Use-case:** Prefer `[GameAssetId<MyAssetType>]` over `[GameAssetId(typeof(MyAssetType))]` on `Guid` fields for conciseness and compile-time type safety when referencing game content such as sprites, sounds, or dialogue assets.

**Implements:** _[GameAssetIdAttribute](../../Murder/Attributes/GameAssetIdAttribute.html)_

### ⭐ Constructors
```csharp
public GameAssetIdAttribute<T>()
```

Creates a new instance with the asset type inferred from `T` and inheritance disabled by default.

### ⭐ Properties
#### AllowInheritance
```csharp
public readonly bool AllowInheritance;
```

Whether the editor picker should also list assets that derive from `T`, not just exact type matches.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### AssetType
```csharp
public readonly Type AssetType;
```

The `GameAsset` subtype that the decorated `Guid` field references, derived from the generic parameter `T`.

**Returns** \
[Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
#### TypeId
```csharp
public virtual Object TypeId { get; }
```

Unique type identifier for this attribute, inherited from `System.Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \


⚡
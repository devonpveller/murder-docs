# GameAssetIdAttribute

**Namespace:** Murder.Attributes \
**Assembly:** Murder.dll

```csharp
public class GameAssetIdAttribute : Attribute
```

This is an attribute used for a field guid that point to a game asset id.

**Intent:** Mark a `Guid` field as a reference to a specific `GameAsset` subtype so the editor renders an asset-type-filtered picker widget.

**Use-case:** Apply to `Guid` fields in components and assets that hold references to game content such as sprites, sounds, or dialogue assets. Set `allowInheritance: true` to allow the picker to include derived asset types.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors

```csharp
public GameAssetIdAttribute(Type type, bool allowInheritance)
```

Creates a new [GameAssetIdAttribute](../../Murder/Attributes/GameAssetIdAttribute.html).

**Parameters** \
`type` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
\
`allowInheritance` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
\

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

#### TypeId

```csharp
public virtual Object TypeId { get; }
```

Unique type identifier for this attribute, inherited from `System.Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

⚡

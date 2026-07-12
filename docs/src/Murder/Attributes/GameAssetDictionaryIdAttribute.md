# GameAssetDictionaryIdAttribute

**Namespace:** Murder.Attributes \
**Assembly:** Murder.dll

```csharp
public class GameAssetDictionaryIdAttribute : Attribute
```

This is an attribute used for a dictionary with a guid on both the key and values.

**Intent:** Instruct the editor to treat a dictionary field as a `Guid`→`Guid` mapping where both keys and values reference specific `GameAsset` subtypes.

**Use-case:** Apply to dictionary fields in components or assets that map one asset type to another (e.g., a character `Guid` mapped to a dialogue asset `Guid`). The editor will show asset-type-aware pickers for both key and value slots.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors

```csharp
public GameAssetDictionaryIdAttribute(Type key, Type value)
```

Creates a new [GameAssetDictionaryIdAttribute](../../Murder/Attributes/GameAssetDictionaryIdAttribute.html).

**Parameters** \
`key` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
`value` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

### ⭐ Properties

#### Key

```csharp
public readonly Type Key;
```

The type of the game asset key.

**Returns** \
[Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

#### TypeId

```csharp
public virtual Object TypeId { get; }
```

Unique type identifier for this attribute, inherited from `System.Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

#### Value

```csharp
public readonly Type Value;
```

The type of the game asset value.

**Returns** \
[Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

⚡

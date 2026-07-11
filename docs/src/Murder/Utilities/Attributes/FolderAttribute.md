# FolderAttribute

**Namespace:** Murder.Utilities.Attributes \
**Assembly:** Murder.dll

```csharp
public class FolderAttribute : Attribute
```

Marks a `GameAsset` subclass with the editor folder it belongs to.

**Intent:** Specifies the editor folder category for a `GameAsset` subclass.

**Use-case:** Apply to a `GameAsset` subclass to control where it appears in the editor asset browser folder hierarchy.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public FolderAttribute()
```

### ⭐ Properties
#### TypeId
```csharp
public virtual Object TypeId { get; }
```

Unique object identity for this attribute type, inherited from `Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \


⚡
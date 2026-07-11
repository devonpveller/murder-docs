# AtlasCoordinatesAttribute

**Namespace:** Murder.Attributes \
**Assembly:** Murder.dll

```csharp
public class AtlasCoordinatesAttribute : Attribute
```

This is an attribute used for field strings that point to an atlas texture.

**Intent:** Mark a string field as a reference to a sprite atlas coordinate name so the editor renders an atlas-aware texture picker.

**Use-case:** Apply to string fields in components or assets that identify a sub-image within a sprite atlas. The editor will display a visual texture browser filtered to atlas entries instead of a plain text input.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public AtlasCoordinatesAttribute()
```

Creates a new instance of `AtlasCoordinatesAttribute`.

### ⭐ Properties
#### TypeId
```csharp
public virtual Object TypeId { get; }
```

Unique type identifier for this attribute, inherited from `System.Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \


⚡
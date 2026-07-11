# SimpleTextureAttribute

**Namespace:** Murder.Attributes \
**Assembly:** Murder.dll

```csharp
public class SimpleTextureAttribute : Attribute
```

Marks a string field as a path to a standalone (non-atlas) texture file, enabling the editor to show a texture file picker.

**Intent:** Signal to the editor that a string field holds a reference to a plain texture file not managed through the sprite atlas system.

**Use-case:** Apply to string fields in components or assets that reference loose texture files, such as background images or UI textures loaded directly at runtime outside of the atlas pipeline.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public SimpleTextureAttribute()
```

Creates a new instance of `SimpleTextureAttribute`.

### ⭐ Properties
#### TypeId
```csharp
public virtual Object TypeId { get; }
```

Unique type identifier for this attribute, inherited from `System.Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \


⚡
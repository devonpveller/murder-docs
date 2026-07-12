# SimpleTextureAttribute

**Namespace:** Murder.Attributes \
**Assembly:** Murder.dll

```csharp
public class SimpleTextureAttribute : Attribute
```

Marks a string field as the identifier of a standalone (non-atlas) texture, so the editor shows a picker combo listing the engine's registered unique textures alongside a live preview image, instead of a plain text box.

**Intent:** Signal to the editor that a string field holds a reference to a plain texture that is registered directly with the texture manager rather than a sprite drawn from a sprite atlas.

**Use-case:** Apply to string fields in components or assets that reference loose textures outside the atlas pipeline. `StringField` checks for this attribute before rendering the field and, when present, draws a combo box built from `Architect.EditorData.AvailableUniqueTextures` plus a preview thumbnail, so designers pick an existing registered texture instead of typing a raw string.

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

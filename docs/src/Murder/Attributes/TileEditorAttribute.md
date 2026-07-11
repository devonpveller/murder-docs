# TileEditorAttribute

**Namespace:** Murder.Attributes \
**Assembly:** Murder.dll

```csharp
public class TileEditorAttribute : Attribute
```

Attribute for systems which will show up in the "Tile Editor" mode.

**Intent:** Mark an editor system class as belonging to the Tile Editor mode so it is only active when the user is painting or editing tile maps.

**Use-case:** Apply to tile-painting, tile-selection, or tile-preview systems that should only run while the Tile Editor mode is active, preventing them from interfering with other editor contexts such as the standard entity editor.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public TileEditorAttribute()
```

Creates a new instance of `TileEditorAttribute`.

### ⭐ Properties
#### TypeId
```csharp
public virtual Object TypeId { get; }
```

Unique type identifier for this attribute, inherited from `System.Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \


⚡
# AtlasNameAttribute

**Namespace:** Murder.Utilities.Attributes \
**Assembly:** Murder.dll

```csharp
public class AtlasNameAttribute : Attribute
```

Marks a [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) field as a reference to the name/key of a currently loaded texture atlas.

**Intent:** Lets a field pick a loaded atlas by its key with editor support, instead of typing the raw atlas identifier by hand.

**Use-case:** Apply to a `string` field used to identify a texture atlas, such as [ReferencedAtlas](../../../Murder/Data/ReferencedAtlas.html)'s `Id` field. When present, the editor's `StringField` replaces the raw text input with a combo box listing the keys of `Game.Data.LoadedAtlasses`, so designers pick a loaded atlas by name instead of risking a typo that would fail to resolve at runtime.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors

```csharp
public AtlasNameAttribute()
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

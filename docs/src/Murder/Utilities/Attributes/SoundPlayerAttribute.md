# SoundPlayerAttribute

**Namespace:** Murder.Utilities.Attributes \
**Assembly:** Murder.dll

```csharp
public class SoundPlayerAttribute : Attribute
```

Attribute used for IComponent structs that will change according to 
            a "story". This is used for debugging and filtering in editor.

**Intent:** Marks a field as a sound player or bank reference.

**Use-case:** Apply to a string field in a component to display a sound player or bank selector in the editor.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public SoundPlayerAttribute()
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
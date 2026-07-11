# SoundAttribute

**Namespace:** Murder.Utilities.Attributes \
**Assembly:** Murder.dll

```csharp
public class SoundAttribute : Attribute
```

Attribute used for IComponent structs that will change according to 
            a "story". This is used for debugging and filtering in editor.

**Intent:** Marks a field as a sound event reference, showing a sound picker in the editor.

**Use-case:** Apply to a `SoundEventId` or compatible field in a component so the editor replaces the raw input with a sound event browser.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public SoundAttribute()
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
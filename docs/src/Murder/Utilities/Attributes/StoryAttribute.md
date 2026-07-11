# StoryAttribute

**Namespace:** Murder.Utilities.Attributes \
**Assembly:** Murder.dll

```csharp
public class StoryAttribute : Attribute
```

Attribute used for IComponent structs that will change according to 
            a "story". This is used for debugging and filtering in editor.

**Intent:** Marks a field as a dialogue story or situation reference.

**Use-case:** Apply to a field in a component to show a dialogue story/situation picker in the editor.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public StoryAttribute()
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
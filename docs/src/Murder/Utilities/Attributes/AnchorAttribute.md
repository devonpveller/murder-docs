# AnchorAttribute

**Namespace:** Murder.Utilities.Attributes \
**Assembly:** Murder.dll

```csharp
public class AnchorAttribute : Attribute
```

Attribute for string fields that are actually an anchor of a state machine.

**Intent:** Marks a string field as a state machine anchor reference.

**Use-case:** Apply to a string field in a component to indicate it stores the name of an anchor within a cutscene or state machine; the editor will show a picker for available anchors.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public AnchorAttribute()
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
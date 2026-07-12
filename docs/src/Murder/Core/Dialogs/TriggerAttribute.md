# TriggerAttribute

**Namespace:** Murder.Core.Dialogs \
**Assembly:** Murder.dll

```csharp
public class TriggerAttribute : Attribute
```

Attribute of fields that should be immediately set off once they are
turned on.

**Intent:** Marks a boolean blackboard field as a one-shot trigger so the engine automatically resets it to `false` after it has been read as `true`, ensuring trigger semantics rather than persistent state.

**Use-case:** Annotate a `bool` field in a custom `IBlackboard` class with `[Trigger]` to indicate that it should fire once and then reset — useful for events like "player just entered room" flags.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors

```csharp
public TriggerAttribute()
```

Creates the trigger attribute with no additional parameters.

### ⭐ Properties

#### TypeId

```csharp
public virtual Object TypeId { get; }
```

Inherited from `Attribute`; returns a unique object that identifies this attribute type instance.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

⚡

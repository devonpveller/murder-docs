# DefaultEditorSystemAttribute

**Namespace:** Murder.Attributes \
**Assembly:** Murder.dll

```csharp
public class DefaultEditorSystemAttribute : Attribute
```

Attributes for fields that should always show up in the editor.
            Commonly used for private fields.

**Intent:** Mark an editor system class as enabled by default so it is automatically activated when the Murder editor initializes.

**Use-case:** Apply to editor system classes that provide core edit-mode functionality. Use `StartActive = false` to register a system that exists but must be manually toggled on by the user.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public DefaultEditorSystemAttribute()
```

Creates a new instance with `StartActive` set to `true`.

```csharp
public DefaultEditorSystemAttribute(bool startActive)
```

Creates a new instance specifying whether the system begins in the active state.

**Parameters** \
`startActive` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

### ⭐ Properties
#### StartActive
```csharp
public readonly bool StartActive;
```

Whether the system should begin in the active (enabled) state when the editor loads.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### TypeId
```csharp
public virtual Object TypeId { get; }
```

Unique type identifier for this attribute, inherited from `System.Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \


⚡
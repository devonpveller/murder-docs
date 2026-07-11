# OnlyShowOnDebugViewAttribute

**Namespace:** Murder.Editor.Attributes \
**Assembly:** Murder.dll

```csharp
public class OnlyShowOnDebugViewAttribute : Attribute
```

Indicates that a system will only be displayed on debug.

**Intent:** Hides a component or property from the editor inspector unless debug view is enabled.

**Use-case:** Apply to components or properties that should only be visible to developers during debugging, keeping the editor UI clean in normal mode.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public OnlyShowOnDebugViewAttribute()
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
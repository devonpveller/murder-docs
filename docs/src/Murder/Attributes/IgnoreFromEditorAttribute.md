# IgnoreFromEditorAttribute

**Namespace:** Murder.Attributes \
**Assembly:** Murder.dll

```csharp
public class IgnoreFromEditorAttribute : Attribute
```

Force ignore a system from showing up in the diagnostics stage.

**Intent:** Opt a specific [ISystem](../../Bang/Systems/ISystem.html) back out of the editor stage even when it would otherwise be auto-registered by [DefaultEditorSystemAttribute](../../Murder/Attributes/DefaultEditorSystemAttribute.html).

**Use-case:** Apply to editor systems that should exist in code (and carry `[DefaultEditorSystem]`) but must be excluded from a particular editor scan — `StageHelpers` checks for this attribute while building the editor stage and skips any system that has it, regardless of the other editor-related attributes it also carries.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors

```csharp
public IgnoreFromEditorAttribute()
```

Creates a new instance of `IgnoreFromEditorAttribute`.

### ⭐ Properties

#### TypeId

```csharp
public virtual Object TypeId { get; }
```

Unique type identifier for this attribute, inherited from `System.Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

⚡

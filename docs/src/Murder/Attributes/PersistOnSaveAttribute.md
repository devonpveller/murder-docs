# PersistOnSaveAttribute

**Namespace:** Murder.Attributes \
**Assembly:** Murder.dll

```csharp
public class PersistOnSaveAttribute : Attribute
```

Overrides any other attribute and make sure this component is persisted in
the entity serialization.

**Intent:** Force a component to be written to the save file even when other persistence-exclusion attributes are also present on the entity.

**Use-case:** Apply to components that must always be saved regardless of other save-exclusion rules. `SavedWorldBuilder` checks for this attribute before honoring `DoNotPersistOnSaveAttribute` or `RuntimeOnlyAttribute` on the same component type, so tagging a component with `PersistOnSaveAttribute` guarantees it survives serialization even if it would otherwise be filtered out.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors

```csharp
public PersistOnSaveAttribute()
```

Creates a new instance of `PersistOnSaveAttribute`.

### ⭐ Properties

#### TypeId

```csharp
public virtual Object TypeId { get; }
```

Unique type identifier for this attribute, inherited from `System.Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

⚡

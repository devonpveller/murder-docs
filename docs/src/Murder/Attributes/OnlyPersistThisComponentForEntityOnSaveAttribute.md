# OnlyPersistThisComponentForEntityOnSaveAttribute

**Namespace:** Murder.Attributes \
**Assembly:** Murder.dll

```csharp
public class OnlyPersistThisComponentForEntityOnSaveAttribute : Attribute
```

This gets rather complicated, but this will persist only one component for the entity in the save.
These are for cases that we want to persist an entity id for an entity with a specific property,
e.g. the player.

**Intent:** Limit save-game serialization for an entity to only the component that carries this attribute, discarding all others for that entity.

**Use-case:** Apply to a special cross-reference component (such as a “player reference” component) that uniquely identifies an entity across scenes. The save system writes only this component, keeping the save file minimal while preserving the entity reference.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors

```csharp
public OnlyPersistThisComponentForEntityOnSaveAttribute()
```

Creates a new instance of `OnlyPersistThisComponentForEntityOnSaveAttribute`.

### ⭐ Properties

#### TypeId

```csharp
public virtual Object TypeId { get; }
```

Unique type identifier for this attribute, inherited from `System.Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

⚡

# MurderTargetedAction

**Namespace:** Murder.Core.MurderActions \
**Assembly:** Murder.dll

```csharp
public sealed struct MurderTargetedAction
```

An authored action that points to a target entity (by asset GUID) and carries a list of interactions to execute against it.

**Intent:** Design-time data that binds an interaction sequence to a specific target entity, used in rule-based and trigger systems.

**Use-case:** Stored in interaction components or rule assets; at runtime the engine resolves the `Target` GUID to an entity ID and executes each item in `Interaction`.

### ⭐ Constructors

```csharp
public MurderTargetedAction()
```

Creates an empty `MurderTargetedAction` with no target and no interactions.

### ⭐ Properties

#### Interaction

```csharp
public readonly ImmutableArray<T> Interaction;
```

The ordered list of interactions to execute against the target entity.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### Target

```csharp
public readonly Guid Target;
```

The asset GUID of the entity that the interactions should be applied to.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

⚡

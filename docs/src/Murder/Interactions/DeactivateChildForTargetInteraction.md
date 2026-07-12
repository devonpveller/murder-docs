# DeactivateChildForTargetInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct DeactivateChildForTargetInteraction : IInteraction
```

Deactivates (or, optionally, activates) a single named child of a target entity resolved from the interacted entity's target reference.

**Intent:** Toggles a named child on a separate target entity, not on the interacted entity itself.

**Use-case:** Unlike [EnableChildrenInteraction](../../Murder/Interactions/EnableChildrenInteraction.html) (which acts on all children of the interacted entity itself), this variant first resolves a separate target entity — useful when the entity being interacted with (e.g. a lever) needs to toggle a child on a completely different entity (e.g. a door somewhere else in the level).

**Implements:** _[IInteraction](../../Bang/Interactions/IInteraction.html)_

### ⭐ Constructors

```csharp
public DeactivateChildForTargetInteraction()
```

### ⭐ Properties

#### ActivateInstead

```csharp
public readonly bool ActivateInstead;
```

When `true`, the named child is activated instead of deactivated.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### ChildName

```csharp
public readonly string ChildName;
```

Name of the child, on the resolved target entity, to activate or deactivate.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Target

```csharp
public readonly string? Target;
```

Optional name of the target entity to act on. When `null`, falls back to the interacted entity's `IdTargetComponent`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Methods

#### Interact(World, Entity, Entity)

```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```

Resolves the target entity (via `Target` or the interacted entity's id-target), finds its `ChildName` child, and activates or deactivates it depending on `ActivateInstead`. Does nothing if the target or child cannot be resolved.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \

⚡

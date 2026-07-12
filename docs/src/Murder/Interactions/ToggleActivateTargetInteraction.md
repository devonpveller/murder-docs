# ToggleActivateTargetInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct ToggleActivateTargetInteraction : IInteraction
```

Activates or deactivates a named target entity resolved from the interacted entity (or, when present, from the entity referenced by the interacted entity's `IdTarget`).

**Intent:** Turns a named target entity on or off as a consequence of an interaction.

**Use-case:** Use to turn machines, lights, or other named entities on/off by name as a consequence of an interaction. The `IdTarget` lookup exists specifically for dialogue-driven interactions, where the original speaker is stored as an id-target rather than being the interacted entity itself.

**Implements:** _[IInteraction](../../Bang/Interactions/IInteraction.html)_

### ⭐ Constructors

```csharp
public ToggleActivateTargetInteraction()
```

### ⭐ Properties

#### Activate

```csharp
public readonly bool Activate;
```

When `true` (the default), the resolved target is activated; when `false`, it is deactivated.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Target

```csharp
public readonly string Target;
```

Name of the target entity, resolved relative to the entity being looked at, to activate or deactivate.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Methods

#### Interact(World, Entity, Entity)

```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```

If the interacted entity has an `IdTarget` (as is the case for dialogue entities, where the original speaker is recorded there), that entity is used to look up `Target`; otherwise the interacted entity itself is used. Once resolved, the named target is activated or deactivated according to `Activate`. Does nothing if no entity or target can be resolved.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \

⚡

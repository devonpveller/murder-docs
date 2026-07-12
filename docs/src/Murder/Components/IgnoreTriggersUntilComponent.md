# IgnoreTriggersUntilComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct IgnoreTriggersUntilComponent : IComponent
```

Ignores all trigger collisions until a time is reached, then it gets removed

**Intent:** Temporarily suppress an entity's participation in trigger/collision interactions for a specified duration.

**Use-case:** Add immediately after an entity exits a trigger zone (or spawns inside one) to provide a brief cooldown before it can re-enter and re-trigger the same interaction.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public IgnoreTriggersUntilComponent(float until)
```

**Parameters** \
`until` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties

#### Until

```csharp
public readonly float Until;
```

Absolute game time (in seconds) after which trigger collisions are no longer ignored and this component is removed.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

⚡

# IgnoreUntilComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct IgnoreUntilComponent : IComponent
```

Useful for tagging an entity for some systems until X time

**Intent:** Temporarily exclude an entity from system processing or interaction until a specified game time is reached.

**Use-case:** Add with the desired expiry time to make systems skip this entity (e.g. during a spawn invincibility window); the system that watches for this component removes it automatically once `Until` is passed.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public IgnoreUntilComponent(float until)
```

Creates a component that tags the entity as ignored until `until`, with interactions disallowed for the duration (`AllowInteract` defaults to `false`).

**Parameters** \
`until` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

```csharp
public IgnoreUntilComponent(bool allowInteract, float until)
```

Creates a component that tags the entity as ignored until `until`, while explicitly controlling whether it may still be interacted with in the meantime via `allowInteract`.

**Parameters** \
`allowInteract` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`until` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties

#### AllowInteract

```csharp
public readonly bool AllowInteract;
```

Whether interactions with this entity are still allowed while the component is present. This is sometimes the case when a system wants to stop displaying an entity, but still give the player feedback that it was interacted with.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Until

```csharp
public readonly float Until;
```

When to remove this component. A negative value will never be automatically removed.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

⚡

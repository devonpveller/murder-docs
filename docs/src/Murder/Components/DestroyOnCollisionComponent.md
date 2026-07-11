# DestroyOnCollisionComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct DestroyOnCollisionComponent : IComponent
```

Destroys (or kills) this entity the moment it collides with another entity.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Automates one-hit destruction of projectiles or fragile objects upon impact.

**Use-case:** Attach to a bullet or hazard entity; `DestroyOnCollisionSystem` will destroy it on the first physics overlap, or send a `FatalDamageMessage` instead when `KillInstead` is `true`.

### ⭐ Properties
#### KillInstead
```csharp
public readonly bool KillInstead;
```

When `true`, sends a `FatalDamageMessage` to the entity instead of immediately destroying it, allowing damage systems to handle the kill.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \


⚡
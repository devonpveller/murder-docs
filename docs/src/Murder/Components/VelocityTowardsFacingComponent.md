# VelocityTowardsFacingComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct VelocityTowardsFacingComponent : IComponent
```

One-shot trigger that converts the entity's current facing direction into a launch velocity.

**Intent:** Let designers/gameplay code launch an entity in whatever direction it is currently facing, without manually computing the direction vector from the facing angle.

**Use-case:** Attach to an entity that already has a `FacingComponent` (e.g. a projectile or a character about to dash) to launch it forward at `Velocity` pixels per second. `VelocityTowardsFacingSystem` reacts to this component being added, immediately converts it into a [VelocityComponent](../../Murder/Components/VelocityComponent.html) pointing along the entity's current facing angle, and then removes this component again — it does not persist on the entity or continuously track facing changes, so it must be re-added to trigger another launch.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public VelocityTowardsFacingComponent()
```

Creates the component with a default velocity of `0`. There is no public constructor that sets `Velocity` directly; it is intended to be authored via the component's field editor (e.g. in the level/prefab editor) or set through reflection.

### ⭐ Properties

#### Velocity

```csharp
public readonly float Velocity;
```

Speed, in pixels per second, to launch the entity at along its current facing direction.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

⚡

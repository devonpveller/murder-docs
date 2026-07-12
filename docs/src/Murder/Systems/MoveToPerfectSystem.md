# MoveToPerfectSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class MoveToPerfectSystem : IFixedUpdateSystem, IStartupSystem, ISystem
```

Moves any entity that has a [MoveToPerfectComponent](../../Murder/Components/MoveToPerfectComponent.html) from its recorded start position to a target position over a fixed duration, using an easing curve instead of velocity/impulse-based physics.

**Intent:** Provides precise, deterministic, eased movement from a start position to a target for entities that should not be pushed around by velocity-based physics (e.g. cutscene actors, moving platforms, scripted props). Because the position is directly interpolated every fixed update, the motion always lands exactly on `Target` at the end of `Duration`, regardless of collisions or friction.

**Use-case:** Add a `MoveToPerfectComponent` (via `Entity.SetMoveToPerfect`) to any entity that needs to glide smoothly to a destination with a configurable [EaseKind](../../Murder/Utilities/EaseKind.html). Optionally set `MoveToPerfectSettings.AvoidActors` so the moving entity pushes actor-layer colliders out of its way (minimum translation vector) instead of overlapping them, which is useful for moving platforms that carry or nudge the player.

**Implements:** _[IFixedUpdateSystem](../../Bang/Systems/IFixedUpdateSystem.html), [IStartupSystem](../../Bang/Systems/IStartupSystem.html), [ISystem](../../Bang/Systems/ISystem.html)_

### ⭐ Constructors

```csharp
public MoveToPerfectSystem()
```

### ⭐ Methods

#### Start(Context)

```csharp
public virtual void Start(Context context)
```

Runs once when the system is added to the world; any entity that already has a `MoveToPerfectComponent` at that point is snapped immediately to its `Target` position and the component is removed. This avoids a pop-in interpolation on scenes that are loaded with entities mid-move, since there is no meaningful "start" time to interpolate from.

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \

#### FixedUpdate(Context)

```csharp
public virtual void FixedUpdate(Context context)
```

For each entity with a `MoveToPerfectComponent`, lazily records the entity's current global position as `StartPosition` the first time it is processed, then evaluates the configured `EaseKind` against the elapsed fraction of `Duration` and sets the entity's global position to the interpolated point between `StartPosition` and `Target`. If `MoveToPerfectSettings.AvoidActors` is set, it also resolves overlaps against actor-layer colliders by pushing them out along the minimum translation vector. Once the eased delta reaches `1` (the duration has elapsed), the `MoveToPerfectComponent` and any `IsStuckComponent` are removed from the entity.

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \

⚡

# FadeWhenInAreaComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct FadeWhenInAreaComponent : IComponent
```

Declares that an entity's sprite should fade in or out based on area overlap; for now, this is only supported for aseprite components.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Describes fade-on-overlap behavior (e.g. foliage, walls, or foreground elements that should become transparent when the player walks behind them) as pure data. It requires a [ColliderComponent](../../Murder/Components/ColliderComponent.html) on the same entity (enforced via `[Requires(typeof(ColliderComponent))]`), since the fade is meant to be triggered by another entity overlapping that collider. The base Murder engine does not ship a system that reads this component — it is intended to be interpreted by a project-specific system that checks collisions against `AppliesTo` and drives the entity's alpha accordingly.

**Use-case:** Attach to foliage, walls, or foreground elements together with a `ColliderComponent`; configure `Style` to control whether the entity hides while something is inside the area, shows only while something is inside, or hides permanently after the first entry, `Duration` for how long the fade transition should take, `AppliesTo` to restrict which entity names/tags trigger it (empty means any), and `FadeChildren` to also fade the entity's children.

### ⭐ Constructors

```csharp
public FadeWhenInAreaComponent()
```

Creates the component with its default values: `Duration` of `0`, `Style` of `HideWhenInArea`, an empty `AppliesTo` list, and `FadeChildren` of `false`.

### ⭐ Properties

#### AppliesTo

```csharp
public readonly ImmutableArray<T> AppliesTo;
```

Names of the child entities or tags that trigger this fade when they enter the area; an empty list applies to all entities.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### Duration

```csharp
public readonly float Duration;
```

Time in seconds over which the fade transition completes.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### FadeChildren

```csharp
public readonly bool FadeChildren;
```

When `true`, child entities of this entity are also faded along with the parent.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Style

```csharp
public readonly FadeWhenInAreaStyle Style;
```

Controls whether the entity hides when inside the area, shows when inside it, or permanently hides after the first entry.

**Returns** \
[FadeWhenInAreaStyle](../../Murder/Components/FadeWhenInAreaStyle.html) \

⚡

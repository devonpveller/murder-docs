# OverrideReflectionComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct OverrideReflectionComponent : IComponent
```

Intended to override (usually temporarily) the `Offset` value of an entity's [ReflectionComponent](../../Murder/Components/Graphics/ReflectionComponent.html) without touching the base component itself.

**Intent:** Hidden from the editor's component picker (`[HideInEditor]`) since it is meant to be added/removed by code rather than authored by hand on a prefab — the intended pattern is a system temporarily nudging where a reflection is drawn (e.g. during a scripted camera or water-surface effect) without disturbing the entity's authored `ReflectionComponent`. **As of this writing, no render system reads this component** — it has no observable effect; treat it as an unwired extension point rather than a working feature.

**Use-case:** Not currently functional; do not rely on this component to change reflection rendering. If you need to adjust a reflection's offset, modify `ReflectionComponent.Offset` directly.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public OverrideReflectionComponent()
```

Creates an override with no offset (0, 0).

```csharp
public OverrideReflectionComponent(Vector2 offset)
```

**Parameters** \
`offset` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

### ⭐ Properties

#### Offset

```csharp
public readonly Vector2 Offset;
```

Pixel offset intended to override the entity's `ReflectionComponent.Offset` while this component is present.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

⚡

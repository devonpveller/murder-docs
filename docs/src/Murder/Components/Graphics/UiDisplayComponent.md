# UiDisplayComponent

**Namespace:** Murder.Components.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct UiDisplayComponent : IComponent
```

Overrides how `SpriteRenderSystem` computes an entity's draw-order sort key, replacing the normal position-based Y-sort with a fixed, explicit value. Marked `[DoNotPersistEntityOnSave]`, so any entity carrying it is excluded from save data.

**Intent:** Regular world sprites are sorted by their Y position (plus small per-entity jitter) so that "further down the screen" draws on top — that's meaningless for UI/HUD elements, which don't live in world space. `SpriteRenderSystem` checks `e.HasUiDisplay()` and, when present, uses `e.GetUiDisplay().YSort` directly as the sort value instead of computing one from the entity's position, letting UI elements be layered deterministically regardless of where they happen to sit in the world.

**Use-case:** Add to HUD or overlay entities (health bars, dialogue boxes, screen-space icons, etc.) that need predictable draw order that isn't derived from their world position; set `YSort` to control stacking relative to other `UiDisplayComponent` entities and to regular world sprites, which are compared against the same sort value.

**Implements:** _[IComponent](../../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public UiDisplayComponent()
```

### ⭐ Properties

#### YSort

```csharp
public readonly float YSort;
```

Sorting offset applied within the UI layer to control draw order relative to other UI entities.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

⚡

# SpriteFrameComponent

**Namespace:** Murder.Components.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct SpriteFrameComponent : IComponent
```

Forces an entity's sprite to render a single, explicit frame of a named animation instead of evaluating the animation over elapsed time.

**Intent:** `SpriteRenderSystem` normally computes which frame to draw from the animation's own timing. When an entity has this component and its `Animation` matches the sprite's `SpriteComponent.CurrentAnimation`, the system instead forces `Frame` as the exact frame index to draw, and uses `Y` in place of the entity's world Y position when computing the draw-order sort key. If `Animation` doesn't match the sprite's current animation, this component is silently ignored for that frame.

**Use-case:** Use when you need to pin a sprite to a specific, known animation frame rather than letting it play back automatically — for example, a UI preview of an item's icon frame, a paused/staged animation sequence driven by scripted logic, or synchronizing a sprite's frame to some other piece of state. For animations that should scrub continuously based on an external 0-1 progress value instead of a fixed frame, use [ForceSpriteDrawAtRatioComponent](../../../Murder/Components/ForceSpriteDrawAtRatioComponent.html) instead.

**Implements:** _[IComponent](../../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public SpriteFrameComponent(string animation, int frame, float y)
```

**Parameters** \
`animation` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`frame` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties

#### Animation

```csharp
public readonly string Animation;
```

Name of the animation this frame override applies to. The override is only applied while this matches the sprite's currently playing animation.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Frame

```csharp
public readonly int Frame;
```

Explicit frame index to force, instead of the frame computed from elapsed animation time.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Y

```csharp
public readonly float Y;
```

Value used in place of the entity's world Y position when computing the draw-order sort key while this override is active.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

⚡

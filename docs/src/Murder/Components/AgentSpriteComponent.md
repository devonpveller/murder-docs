# AgentSpriteComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct AgentSpriteComponent : IComponent
```

Configures which sprite asset and animation name prefixes an agent entity uses for idle and walk states.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Links an agent entity to a `SpriteAsset` and defines the naming convention (idle/walk prefixes) used to pick the right directional animation clip for that agent. Declares `[Requires(typeof(FacingComponent))]`, so adding this component also requires the entity to have a `FacingComponent` — the two are read together to select which clip suffix (direction) to play.

**Use-case:** Attach to any entity with an `AgentComponent`; `AgentSpriteSystem` reads `AnimationGuid`, `IdlePrefix`/`WalkPrefix`, and the entity's `FacingComponent`/velocity to decide whether to play e.g. `"idle_right"` or `"walk_down"`, and renders into `TargetSpriteBatch` at `YSortOffset`. Use `WithIdleAndWalkPrefix` to swap animation naming conventions (e.g. for a costume or transformation) without touching the other fields.

### ⭐ Constructors

```csharp
public AgentSpriteComponent()
```

Default constructor: `AnimationGuid` is `Guid.Empty` (no sprite assigned), `TargetSpriteBatch` defaults to `Batches2D.GameplayBatchId`, `IdlePrefix` is `"idle"`, and `WalkPrefix` is `"walk"`.

```csharp
public AgentSpriteComponent(Guid animationGuid, int targetSpriteBatch, int ySortOffset, string idlePrefix, string walkPrefix)
```

Creates a fully configured component pointing at a specific sprite asset, render batch, sort offset, and animation-name prefixes.

**Parameters** \
`animationGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`targetSpriteBatch` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`ySortOffset` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`idlePrefix` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`walkPrefix` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Properties

#### AnimationGuid

```csharp
public Guid AnimationGuid { get; public set; }
```

GUID of the `SpriteAsset` (tagged via `[GameAssetId(typeof(SpriteAsset))]` so the editor renders an asset picker) that contains the agent's idle and walk animation clips. `Guid.Empty` means no sprite is assigned.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### TargetSpriteBatch

```csharp
public readonly int TargetSpriteBatch;
```

Index (tagged `[SpriteBatchReference]`) of the [Batches2D](../../Murder/Core/Graphics/Batches2D.html) sprite batch that this agent's sprite is drawn into; defaults to `Batches2D.GameplayBatchId`.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### YSortOffset

```csharp
public readonly int YSortOffset { get; public set; }
```

Extra pixel offset added when computing this entity's Y-sort draw order, letting an agent's sprite be nudged in front of or behind other sprites near the same Y position without moving the entity itself.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### IdlePrefix

```csharp
public readonly string IdlePrefix;
```

Prefix used to build the idle animation clip name, combined with the entity's facing direction (e.g., `"idle"` selects `"idle_right"`, `"idle_up"`, etc. when the agent is not moving).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### WalkPrefix

```csharp
public readonly string WalkPrefix;
```

Prefix used to build the walk animation clip name, combined with the entity's facing direction (e.g., `"walk"` selects `"walk_right"`, `"walk_up"`, etc. while the agent is moving).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Methods

#### WithIdleAndWalkPrefix(string, string)

```csharp
public AgentSpriteComponent WithIdleAndWalkPrefix(string idle, string walk)
```

Returns a copy of this component with `IdlePrefix` and `WalkPrefix` replaced, keeping the same `AnimationGuid`, `TargetSpriteBatch`, and `YSortOffset`.

**Parameters** \
`idle` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`walk` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[AgentSpriteComponent](../../Murder/Components/AgentSpriteComponent.html) \

#### WithIdleAndWalkPrefix(Guid?, string, string)

```csharp
public AgentSpriteComponent WithIdleAndWalkPrefix(Guid? spriteGuid, string idle, string walk)
```

Returns a copy of this component with `IdlePrefix`/`WalkPrefix` replaced and, optionally, a new `AnimationGuid` (passing `null` keeps the current sprite asset).

**Parameters** \
`spriteGuid` [Guid?](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`idle` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`walk` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[AgentSpriteComponent](../../Murder/Components/AgentSpriteComponent.html) \

⚡

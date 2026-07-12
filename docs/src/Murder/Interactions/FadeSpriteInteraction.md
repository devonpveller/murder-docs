# FadeSpriteInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct FadeSpriteInteraction : IInteraction
```

Starts an alpha fade on the interacted entity's sprite, over `FadeDuration` seconds, going from `StartAlpha` to `EndAlpha`.

**Intent:** Triggers an interaction-driven visual fade transition on an entity's sprite.

**Use-case:** Use for interaction-triggered visual transitions, such as fading out a pickup as it is collected, or fading a prop in or out. Internally it attaches a `FadeSpriteComponent` (via the `SetFadeSprite` extension), which a render/update system consumes each frame to animate the sprite's alpha.

**Implements:** _[IInteraction](../../Bang/Interactions/IInteraction.html)_

### ⭐ Constructors

```csharp
public FadeSpriteInteraction()
```

### ⭐ Properties

#### DestroyOnEnd

```csharp
public readonly bool DestroyOnEnd;
```

When `true` (the default), the entity is destroyed once the fade completes — useful for fade-out-then-remove effects. When `false`, the entity is left alone once the fade finishes, keeping its final alpha.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### EndAlpha

```csharp
public readonly float EndAlpha;
```

Sprite alpha at the end of the fade (0 = fully transparent, 1 = fully opaque).

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### FadeDuration

```csharp
public readonly float FadeDuration;
```

How long, in seconds, the fade from `StartAlpha` to `EndAlpha` takes.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### StartAlpha

```csharp
public readonly float StartAlpha;
```

Sprite alpha at the start of the fade (0 = fully transparent, 1 = fully opaque).

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Methods

#### Interact(World, Entity, Entity)

```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```

Attaches a fade-sprite effect to the interacted entity spanning from the current game time to `FadeDuration` seconds later, animating alpha from `StartAlpha` to `EndAlpha`, and optionally flags it to be destroyed once the fade ends. Does nothing if `interacted` is null.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \

⚡

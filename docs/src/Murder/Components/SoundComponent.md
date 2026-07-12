# SoundComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct SoundComponent : IComponent
```

Sound component which will be immediately played and destroyed.

**Intent:** Fire a one-shot sound event from an entity the moment the component is added, using ECS's reactive add/remove flow instead of an imperative "play sound" call.

**Use-case:** Add this component (typically via a dedicated one-off entity) with `Sound` set to the event to play; `SoundsSystem` (`[Watch(typeof(SoundComponent))]`) picks it up in `OnAdded`, calls `SoundServices.Play(sound.Sound.Value, e)` if `Sound` has a value, and then either destroys the entity (if `DestroyEntity` is `true`) or just removes the `SoundComponent` again (if `false`), leaving the rest of the entity intact.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public SoundComponent()
```

```csharp
public SoundComponent(SoundEventId sound, bool destroyEntity)
```

**Parameters** \
`sound` [SoundEventId](../../Murder/Core/Sounds/SoundEventId.html) \
`destroyEntity` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

### ⭐ Properties

#### DestroyEntity

```csharp
public readonly bool DestroyEntity;
```

When true, the entity is destroyed after the sound finishes playing.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Sound

```csharp
public readonly SoundEventId? Sound;
```

Identifier of the sound event `SoundsSystem` plays via `SoundServices.Play` when this component is added. Leaving it `null` (the default) means the entity is processed but nothing is played — useful if only `DestroyEntity` matters for that entity.

**Returns** \
[SoundEventId?](../../Murder/Core/Sounds/SoundEventId.html) \

⚡

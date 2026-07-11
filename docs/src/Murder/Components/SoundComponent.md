# SoundComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct SoundComponent : IComponent
```

Sound component which will be immediately played and destroyed.

**Intent:** Fire a one-shot sound event from an entity the moment the component is added.

**Use-case:** Add this component to an entity (or a dedicated sound entity) when you need to trigger a sound effect; the system plays it immediately and then removes the component or the entity.

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
public readonly T? Sound;
```

Identifier of the sound event to play. Null disables playback.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \


⚡
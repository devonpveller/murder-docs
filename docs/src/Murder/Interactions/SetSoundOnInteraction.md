# SetSoundOnInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct SetSoundOnInteraction : IInteraction
```

Applies sound parameter changes and triggers sound events on interaction.

**Intent:** Modifies sound blackboard parameters and fires sound trigger events when an interaction occurs.

**Use-case:** Use to change audio state on interaction, such as adjusting ambient sound levels or triggering a layered sound transition when the player activates an environmental switch.

**Implements:** _[IInteraction](../../Bang/Interactions/IInteraction.html)_

### ⭐ Constructors
```csharp
public SetSoundOnInteraction()
```

### ⭐ Properties
#### Parameters
```csharp
public readonly ImmutableArray<T> Parameters;
```
Sound parameter actions to apply to the sound middleware on interaction.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
#### Triggers
```csharp
public readonly ImmutableArray<T> Triggers;
```
Sound events to trigger on interaction.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
### ⭐ Methods
#### Interact(World, Entity, Entity)
```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```
Applies all configured parameter changes and fires all sound trigger events.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \



⚡
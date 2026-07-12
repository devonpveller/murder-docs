# FireAfterInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct FireAfterInteraction : IInteraction
```

Fires a list of sub-interactions either immediately or after a delay, via [DialogueServices](../../Murder/Services/DialogueServices.html).

**Intent:** Delays the effect of a trigger by a fixed number of seconds.

**Use-case:** The lightweight way to delay the effect of a trigger without writing a dedicated state machine or system — e.g. waiting a beat before a door slams shut, or staggering the consequences of a scripted event.

**Implements:** _[IInteraction](../../Bang/Interactions/IInteraction.html)_

### ⭐ Constructors

```csharp
public FireAfterInteraction()
```

### ⭐ Properties

#### Actions

```csharp
public readonly ImmutableArray<IInteractiveComponent> Actions;
```

The interactions to fire once `Seconds` have elapsed (or immediately, if it is zero).

**Returns** \
[ImmutableArray\<IInteractiveComponent\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### Seconds

```csharp
public readonly float Seconds;
```

Delay, in seconds, before `Actions` are fired. When zero (the default), the actions fire immediately and synchronously instead of scheduling a delayed callback.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Methods

#### Interact(World, Entity, Entity)

```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```

When `Seconds` is zero, fires `Actions` immediately. Otherwise, schedules them to fire after `Seconds` seconds via a world coroutine.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \

⚡

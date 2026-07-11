# InteractOnCollisionComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct InteractOnCollisionComponent : IComponent
```

Triggers the entity's interactive components when another entity enters (and optionally exits) its collision bounds.

**Intent:** Enable proximity-based interactions, such as opening a door, starting a dialogue, or activating a trap, driven by physical collision overlap.

**Use-case:** Add to a trigger zone entity; configure `PlayerOnly` to restrict activation to the player, `OnlyOnce` to fire only the first time, and `SendMessageOnExit` to also fire when the collider leaves.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public InteractOnCollisionComponent()
```

```csharp
public InteractOnCollisionComponent(bool playerOnly, bool sendMessageOnExit)
```

**Parameters** \
`playerOnly` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`sendMessageOnExit` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

```csharp
public InteractOnCollisionComponent(bool playerOnly)
```

**Parameters** \
`playerOnly` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

### ⭐ Properties
#### CustomEnterMessages
```csharp
public readonly ImmutableArray<T> CustomEnterMessages;
```

Additional interactive components whose interactions are triggered when an actor enters the collision area, in addition to any interactions on this entity.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
#### CustomExitMessages
```csharp
public readonly ImmutableArray<T> CustomExitMessages;
```

Additional interactive components whose interactions are triggered when an actor exits the collision area.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
#### OnlyOnce
```csharp
public readonly bool OnlyOnce;
```

When `true`, the collision interaction fires only the first time an actor enters; subsequent entries are ignored.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### PlayerOnly
```csharp
public readonly bool PlayerOnly;
```

When `true`, only collisions with the player entity trigger the interaction; other actors are ignored.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### SendMessageOnExit
```csharp
public readonly bool SendMessageOnExit;
```

When `true`, the interaction is also triggered when the colliding actor exits the collision area.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### SendMessageOnStay
```csharp
public readonly bool SendMessageOnStay;
```

When `true`, the interaction is repeatedly triggered while the colliding actor remains inside the collision area.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \


⚡
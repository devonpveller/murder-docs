# FatalDamageMessage

**Namespace:** Murder.Messages \
**Assembly:** Murder.dll

```csharp
public sealed struct FatalDamageMessage : IMessage
```

A message signaling that this entity should be killed

**Intent:** Signal to all listening systems that an entity has taken fatal damage and must be destroyed.

**Use-case:** Send this message from a damage system the moment an entity's health reaches zero. Receiving systems can then handle cleanup, loot drops, death animations, or any other on-death behavior.

**Implements:** _[IMessage](../../Bang/Components/IMessage.html)_

### ⭐ Constructors
```csharp
public FatalDamageMessage(Vector2 fromPosition, int damageAmount)
```

**Parameters** \
`fromPosition` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`damageAmount` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties
#### Amount
```csharp
public readonly int Amount;
```

The amount of damage delivered by this fatal hit.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### FromPosition
```csharp
public readonly Vector2 FromPosition;
```

World-space position from which the fatal damage originated, used to calculate knockback or death direction.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \


⚡
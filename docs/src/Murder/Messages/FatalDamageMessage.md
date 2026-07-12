# FatalDamageMessage

**Namespace:** Murder.Messages \
**Assembly:** Murder.dll

```csharp
public sealed struct FatalDamageMessage : IMessage
```

A message signaling that an entity should be killed.

**Intent:** Signal to all listening systems that an entity has taken damage that should result in its death, optionally identifying who dealt the blow and which entity was hit, and optionally suppressing whatever normally happens on death (such as item drops).

**Use-case:** Send this from a damage/health system the moment an entity's health reaches zero, or from any system that wants to force-kill an entity outright. `DestroyOnCollisionSystem` sends it (via the generated `entity.SendFatalDamageMessage()` extension) instead of directly calling `Entity.Destroy()` when a `DestroyOnCollisionComponent` has `KillInstead` set, so death-reaction systems (loot drops, death animations, score, etc.) still get a chance to run. Listening systems can inspect `FromId`/`DamagedEntityId` to know who attacked whom, or check `Flags` to skip specific death behavior (e.g. `IgnoreDrop`).

**Implements:** _[IMessage](../../Bang/Components/IMessage.html)_

### ⭐ Constructors

```csharp
public FatalDamageMessage()
```

Creates a fatal damage notification with no attacker/victim information (`FromId` and `DamagedEntityId` both default to `-1`) and no flags. Used for a generic, unattributed kill.

```csharp
public FatalDamageMessage(FatalDamageFlags flags)
```

Creates a fatal damage notification carrying only [FatalDamageFlags](../../Murder/Messages/FatalDamageFlags.html), leaving `FromId`/`DamagedEntityId` at their `-1` defaults. Use this to force-kill an entity while still controlling secondary behavior, such as passing `IgnoreDrop` to suppress item drops.

**Parameters** \
`flags` [FatalDamageFlags](../../Murder/Messages/FatalDamageFlags.html) \

```csharp
public FatalDamageMessage(int fromId, int damagedEntityId)
```

Creates a fatal damage notification identifying both the entity that caused the damage and the entity that was hit, leaving `Flags` at `FatalDamageFlags.None`. Use this whenever the source of the damage matters, such as for on-kill rewards or combat logs.

**Parameters** \
`fromId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`damagedEntityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties

#### FromId

```csharp
public readonly int FromId;
```

Entity ID of the attacker that caused the fatal damage. Defaults to `-1` when unknown, environmental, or self-inflicted (in which case it may equal `DamagedEntityId`).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### DamagedEntityId

```csharp
public readonly int DamagedEntityId;
```

Entity ID of the entity that was hit. Defaults to `-1`, which listeners should treat as "critical fatal" — i.e. everything present should be considered to have taken the fatal damage, not just one specific entity.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Flags

```csharp
public readonly FatalDamageFlags Flags;
```

Modifiers that change how the fatal damage should be handled, such as suppressing the usual item-drop behavior on death. Defaults to `FatalDamageFlags.None`.

**Returns** \
[FatalDamageFlags](../../Murder/Messages/FatalDamageFlags.html) \

⚡

# AddEntityOnInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct AddEntityOnInteraction : IInteraction
```

Instantiates a [PrefabAsset](../../Murder/Assets/PrefabAsset.html) as a standalone entity in the world when the interaction fires.

**Intent:** Spawns a brand new, independent entity (as opposed to [AddChildOnInteraction](../../Murder/Interactions/AddChildOnInteraction.html), which attaches the new entity as a child) as a consequence of an interaction.

**Use-case:** Use to create projectiles, particle/VFX entities, loot pickups, or other one-off objects at runtime, optionally positioned at the interactor or interacted entity and optionally removing the triggering interaction so it only fires once.

**Implements:** _[IInteraction](../../Bang/Interactions/IInteraction.html)_

### ⭐ Constructors

```csharp
public AddEntityOnInteraction()
```

```csharp
public AddEntityOnInteraction(Guid prefab)
```

**Parameters** \
`prefab` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

### ⭐ Properties

#### CustomComponents

```csharp
public readonly ImmutableArray<IComponent>? CustomComponents;
```

Optional extra components added to (or replacing components on) the newly spawned entity right after creation. Any `IModifiableComponent` in this list is deep-copied first so the same serialized instance can be reused safely across multiple triggers.

**Returns** \
[ImmutableArray\<IComponent\>?](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### Flags

```csharp
public AddEntityFlags Flags { get; init; }
```

Controls where the spawned entity is positioned and whether the triggering interaction removes itself after firing.

**Returns** \
[AddEntityFlags](../../Murder/Interactions/AddEntityFlags.html) \

#### Prefab

```csharp
public readonly Guid Prefab;
```

Asset id of the `PrefabAsset` to instantiate when the interaction fires.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

### ⭐ Methods

#### Interact(World, Entity, Entity)

```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```

Creates the entity referenced by `Prefab`, applies any `CustomComponents`, then positions it at the interactor's or interacted entity's global position depending on `Flags`. If `Flags` includes `RemoveAfterTriggered`, the triggering interaction is removed from the interacted entity afterwards so it only fires once.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \

⚡

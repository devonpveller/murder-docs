# SituationComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct SituationComponent : IComponent
```

Links an entity to a specific dialogue situation within a [CharacterAsset](../../Murder/Assets/Dialogs/CharacterAsset.html), allowing it to start a conversation at a defined entry point.

**Intent:** Store which character and which dialogue branch an interactable entity will trigger.

**Use-case:** Attach to NPC or interactive objects; when a player interacts, the dialogue system reads `Character` and `Situation` to find the correct script to execute.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public SituationComponent()
```

```csharp
public SituationComponent(Guid character, int situation)
```

**Parameters** \
`character` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`situation` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties
#### Character
```csharp
public readonly Guid Character;
```

GUID of the [CharacterAsset](../../Murder/Assets/Dialogs/CharacterAsset.html) whose dialogue this entity triggers.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### Empty
```csharp
public bool Empty { get; }
```

Returns true when no character has been assigned to this situation.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Situation
```csharp
public readonly int Situation;
```

This is the starter situation for the interaction.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
### ⭐ Methods
#### WithSituation(int)
```csharp
public SituationComponent WithSituation(int situation)
```

Returns a new component with the situation identifier replaced by the given value.

**Parameters** \
`situation` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[SituationComponent](../../Murder/Components/SituationComponent.html) \



⚡
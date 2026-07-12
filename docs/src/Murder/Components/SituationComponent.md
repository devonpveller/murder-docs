# SituationComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct SituationComponent : IComponent
```

Links an entity to a specific dialogue situation (an entry point/branch name) within a [CharacterAsset](../../Murder/Assets/CharacterAsset.html), allowing it to start a conversation at a defined point in that character's dialogue graph.

**Intent:** Store which character asset and which named situation (branch) an interactable entity will trigger when talked to.

**Use-case:** `TalkToInteraction` requires (`[Requires(typeof(SituationComponent))]`) this component on any entity the player can talk to; when interacted, it resolves the active `SituationComponent` — either an override pushed via `Entity.SetOverrideSituation`/`OverrideSituationComponent`, or this component's own value — and passes it into `DialogStateMachine`, which reads `Character` and `Situation` to look up the correct dialogue node in `DialogueServices`. Use `WithSituation` to build a modified copy that jumps to a different branch of the same character without touching `Character`.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public SituationComponent()
```

Default constructor used by the ECS/serializer. Produces an empty situation (`Character` is `Guid.Empty`, so `Empty` is `true`) that must be filled in before it is useful for dialogue.

```csharp
public SituationComponent(Guid character, string situation)
```

Creates a situation pointing at the given [CharacterAsset](../../Murder/Assets/CharacterAsset.html) and the named situation (branch) within it to start from.

**Parameters** \
`character` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`situation` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Properties

#### Character

```csharp
public readonly Guid Character;
```

GUID of the [CharacterAsset](../../Murder/Assets/CharacterAsset.html) whose dialogue this entity triggers. Marked with `[GameAssetId(typeof(CharacterAsset))]` so the editor renders it as an asset picker restricted to character assets.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### Empty

```csharp
public bool Empty { get; }
```

Returns `true` when `Character` is still `Guid.Empty`, i.e. no character asset has been assigned to this situation yet. Used to detect an unconfigured/default-constructed component before attempting to resolve dialogue from it.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Situation

```csharp
public readonly string? Situation;
```

Name of the situation (dialogue branch/entry point) within `Character`'s [CharacterAsset](../../Murder/Assets/CharacterAsset.html) that this component starts the conversation at. Defaults to `string.Empty`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Methods

#### WithSituation(string)

```csharp
public SituationComponent WithSituation(string situation)
```

Returns a new component with the same `Character` but the situation name replaced by `situation`, letting game code redirect an entity to a different branch of the same character's dialogue without rebuilding the whole component.

**Parameters** \
`situation` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[SituationComponent](../../Murder/Components/SituationComponent.html) \

⚡

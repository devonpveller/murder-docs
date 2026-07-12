# PickEntityToAddOnStartComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct PickEntityToAddOnStartComponent : IComponent
```

This will trigger an effect by placing [OnMatchPrefab](../../Murder/Components/PickEntityToAddOnStartComponent.html#onmatchprefab) or [OnNotMatchPrefab](../../Murder/Components/PickEntityToAddOnStartComponent.html#onnotmatchprefab) in the world depending on whether associated rule requirements are satisfied at load time.

**Intent:** Conditionally spawn one of two prefabs into the world when the scene is loaded, based on blackboard rule evaluation.

**Use-case:** Attach to an entity together with [InteractOnRuleMatchComponent](../../Murder/Components/InteractOnRuleMatchComponent.html) to have the engine instantiate a different prefab depending on the current game-state (e.g. show a locked or unlocked door).

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public PickEntityToAddOnStartComponent()
```

### ⭐ Properties

#### OnMatchPrefab

```csharp
public readonly Guid OnMatchPrefab;
```

GUID of the prefab asset instantiated when the rule conditions are met.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### OnNotMatchPrefab

```csharp
public readonly Guid OnNotMatchPrefab;
```

GUID of the prefab asset instantiated when the rule conditions are **not** met.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

⚡

# HasVisionComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct HasVisionComponent : IComponent
```

Marks an entity as able to perceive other entities within a grid-tile range, intended for AI vision/detection checks (e.g. whether an enemy notices the player). There is currently no built-in engine system that reads this component; it exists as reusable data for game-specific AI/detection systems to filter on and interpret.

**Intent:** Provide a standard, editor-visible way to author a "vision range" per entity so game-specific detection logic (line of sight, awareness, alerting) has a common data source instead of every game reinventing its own vision component.

**Use-case:** Add to enemies or NPCs and set `Range` (in grid tiles) to control how far they should be able to detect the player or other tagged entities; pair with your own detection/AI system that filters on this component and performs the actual line-of-sight or distance check.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public HasVisionComponent()
```

Creates a vision component with the default range of 10 tiles.

### ⭐ Properties

#### Range

```csharp
public readonly int Range;
```

Vision range, expressed in grid tiles. Entities farther than this distance are considered out of sight.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡

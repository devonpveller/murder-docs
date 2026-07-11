# HasVisionComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct HasVisionComponent : IComponent
```

Marks an entity as capable of perceiving other entities within a tile-based vision range.

**Intent:** Enable AI vision checks so that systems can determine which entities fall within this entity's line-of-sight cone or range.

**Use-case:** Add to enemies or NPCs and set `Range` (in grid tiles) to control how far they can detect the player or other tagged entities.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public HasVisionComponent()
```

### ⭐ Properties
#### Range
```csharp
public readonly int Range;
```

Vision range in grid tiles; entities beyond this distance are not perceived.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \


⚡
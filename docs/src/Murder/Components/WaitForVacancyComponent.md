# WaitForVacancyComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct WaitForVacancyComponent : IComponent
```

Blocks an entity from advancing until the grid cell it needs to occupy becomes unoccupied.

**Intent:** Prevent pathfinding agents from colliding when multiple agents target the same grid cell simultaneously.

**Use-case:** Attach to an agent when it reaches a cell that is still occupied by another entity; it will wait in place and optionally notify its parent when the cell clears.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public WaitForVacancyComponent(bool alertParent)
```

**Parameters** \
`alertParent` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

### ⭐ Properties
#### AlertParent
```csharp
public readonly bool AlertParent;
```

When true, the parent entity is notified when the waited-for cell becomes vacant.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \


⚡
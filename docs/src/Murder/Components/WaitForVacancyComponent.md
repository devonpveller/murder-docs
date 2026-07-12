# WaitForVacancyComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct WaitForVacancyComponent : IComponent
```

Marker/data component intended to flag that an entity is waiting for a grid cell it wants to occupy to become vacant.

**Intent:** Provide a common data shape (a flag plus an "alert parent" option) for pathfinding-style "wait for a cell to clear" behavior, so game-specific systems don't each invent their own component for it.

**Use-case:** Intended to be attached to an agent when it reaches a cell that is still occupied by another entity, so it can wait in place until the cell frees up, optionally notifying its parent when that happens. The core Murder engine does not currently ship a system that reads or acts on this component — it exists purely as a data holder for game-specific or pathfinding logic implemented downstream to add, remove, and interpret.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public WaitForVacancyComponent(bool alertParent)
```

Creates the component, optionally flagging that the parent entity should be alerted once the awaited cell is free.

**Parameters** \
`alertParent` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

### ⭐ Properties

#### AlertParent

```csharp
public readonly bool AlertParent;
```

When `true`, indicates that the parent entity (if any) should be notified once the cell being waited on becomes vacant. Interpretation of this flag is left entirely to whichever consuming system reads it.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

⚡

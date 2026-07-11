# FadeWhenInAreaComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct FadeWhenInAreaComponent : IComponent
```

For now, this is only supported for aseprite components.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Fades an entity's sprite in or out when another entity (typically the player) enters or exits this entity's collision area.

**Use-case:** Attach to foliage, walls, or foreground elements that should become transparent when the player walks behind them; configure `Style`, `Duration`, and `AppliesTo` to control which entities trigger the fade and how quickly.

### ⭐ Constructors
```csharp
public FadeWhenInAreaComponent()
```

### ⭐ Properties
#### AppliesTo
```csharp
public readonly ImmutableArray<T> AppliesTo;
```

Names of the child entities or tags that trigger this fade when they enter the area; an empty list applies to all entities.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
#### Duration
```csharp
public readonly float Duration;
```

Time in seconds over which the fade transition completes.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### FadeChildren
```csharp
public readonly bool FadeChildren;
```

When `true`, child entities of this entity are also faded along with the parent.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Style
```csharp
public readonly FadeWhenInAreaStyle Style;
```

Controls whether the entity hides when inside the area, shows when inside it, or permanently hides after the first entry.

**Returns** \
[FadeWhenInAreaStyle](../../Murder/Components/FadeWhenInAreaStyle.html) \


⚡
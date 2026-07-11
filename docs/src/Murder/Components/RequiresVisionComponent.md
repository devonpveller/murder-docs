# RequiresVisionComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct RequiresVisionComponent : IComponent
```

Will only be rendered if the player has vision on this

**Intent:** Hide an entity's visual representation until the player's vision cone or field of view covers it.

**Use-case:** Attach to hidden objects or enemies in stealth or fog-of-war scenarios; the entity is not rendered until the player can see it, and if `OnlyOnce` is true it stays visible once seen.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Properties
#### OnlyOnce
```csharp
public readonly bool OnlyOnce;
```

When true, the entity remains permanently visible after first entering the player's vision; when false it hides again when vision is lost.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \


⚡
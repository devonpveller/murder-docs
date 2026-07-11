# WorldServices

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public static class WorldServices
```

Extension utilities for querying world-level metadata from a Bang `World`.

**Intent:** Provides helpers that extract Murder-specific information from a generic `World` instance.

**Use-case:** Call `Guid` to retrieve the `Guid` of the current world's asset, useful for save-state tracking and scene comparison.

### ⭐ Methods
#### Guid(World)
```csharp
public Guid Guid(World world)
```
Returns the `Guid` of the world asset that the `MonoWorld` instance was created from.

**Parameters** \
`world` [World](../../Bang/World.html) \

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \



⚡
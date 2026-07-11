# Exploration

**Namespace:** Murder.Assets \
**Assembly:** Murder.dll

```csharp
public class Exploration
```

Configuration data that controls the visual appearance of the fog-of-war / exploration system used by the world map.

**Intent:** Bundle the color and timing parameters that govern how cells of the map transition between unexplored, exploring, and fully-visible states.

**Use-case:** Assign an `Exploration` value inside `GameProfile` to tune how quickly tiles and sprites fade in as the player explores the world, and choose the tint colors for unvisited and currently-revealed areas.

### ⭐ Constructors
```csharp
public Exploration()
```

### ⭐ Properties
#### ExploreColor
```csharp
public Color ExploreColor;
```

Tint color applied to map cells that are currently being revealed (transitioning from unexplored to visible).

**Returns** \
[Color](../../Murder/Core/Graphics/Color.html) \
#### SpriteExplorationDuration
```csharp
public float SpriteExplorationDuration;
```

Duration in seconds for sprite-based map cells to animate from unexplored to the explored state.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### TileExplorationDuration
```csharp
public float TileExplorationDuration;
```

Duration in seconds for tile-based map cells to animate from unexplored to the explored state.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### UnexploredColor
```csharp
public Color UnexploredColor;
```

Tint color applied to map cells that have not yet been visited or revealed by the player.

**Returns** \
[Color](../../Murder/Core/Graphics/Color.html) \


⚡
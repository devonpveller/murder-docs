# DirectionHelper

**Namespace:** Murder.Helpers \
**Assembly:** Murder.dll

```csharp
public static class DirectionHelper
```

Utility methods for converting between `Direction` enum values, angles, vectors, and sprite flip flags.

**Intent:** Centralizes all direction math so game code can convert freely between angle radians, `Vector2` velocities, and the eight-direction enum.

**Use-case:** Use `FromVector` to derive a character's facing direction from its velocity, `ToAngle` to rotate a projectile sprite, and `Flipped`/`GetFlipped` to determine whether a sprite should be horizontally mirrored.

### ⭐ Properties
#### Cardinal4
```csharp
public static ImmutableArray<T> Cardinal4;
```
The four axis-aligned directions: Right, Down, Left, Up.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
#### Cardinal4Flipped
```csharp
public static ImmutableArray<T> Cardinal4Flipped;
```
The four axis-aligned directions in reverse (Up, Left, Down, Right).

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
#### Cardinal8
```csharp
public static ImmutableArray<T> Cardinal8;
```
All eight compass directions in clockwise order starting from Right.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
#### Cardinal8Flipped
```csharp
public static ImmutableArray<T> Cardinal8Flipped;
```
All eight compass directions in counter-clockwise order.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
### ⭐ Methods
#### Flipped(Direction)
```csharp
public bool Flipped(Direction direction)
```
Returns `true` if the given direction requires the sprite to be horizontally flipped.

**Parameters** \
`direction` [Direction](../../Murder/Helpers/Direction.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### FromAngle(float)
```csharp
public Direction FromAngle(float angle)
```

Converts an angle (in radians) to a Direction enum.

**Parameters** \
`angle` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
\

**Returns** \
[Direction](../../Murder/Helpers/Direction.html) \
\

#### FromVector(Vector2)
```csharp
public Direction FromVector(Vector2 vector)
```
Converts a `Vector2` velocity or offset to the closest of the eight `Direction` values.

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Direction](../../Murder/Helpers/Direction.html) \

#### FromVectorWith4Directions(Vector2)
```csharp
public Direction FromVectorWith4Directions(Vector2 vector)
```
Converts a `Vector2` to the closest of the four cardinal `Direction` values (no diagonals).

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Direction](../../Murder/Helpers/Direction.html) \

#### Invert(Direction)
```csharp
public Direction Invert(Direction direction)
```
Returns the opposite of the given direction (e.g. Up → Down, UpLeft → DownRight).

**Parameters** \
`direction` [Direction](../../Murder/Helpers/Direction.html) \

**Returns** \
[Direction](../../Murder/Helpers/Direction.html) \

#### LookAtEntity(Entity, Entity)
```csharp
public Direction LookAtEntity(Entity e, Entity target)
```
Returns the direction from entity `e` toward entity `target`.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \
`target` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[Direction](../../Murder/Helpers/Direction.html) \

#### LookAtPosition(Entity, Vector2)
```csharp
public Direction LookAtPosition(Entity e, Vector2 target)
```
Returns the direction from entity `e` toward world position `target`.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \
`target` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Direction](../../Murder/Helpers/Direction.html) \

#### Random()
```csharp
public Direction Random()
```
Returns a random one of the eight compass directions.

**Returns** \
[Direction](../../Murder/Helpers/Direction.html) \

#### RandomCardinal()
```csharp
public Direction RandomCardinal()
```
Returns a random one of the four cardinal directions (no diagonals).

**Returns** \
[Direction](../../Murder/Helpers/Direction.html) \

#### Reverse(Direction)
```csharp
public Direction Reverse(Direction direction)
```
Returns the opposite of the given direction; alias for `Invert`.

**Parameters** \
`direction` [Direction](../../Murder/Helpers/Direction.html) \

**Returns** \
[Direction](../../Murder/Helpers/Direction.html) \

#### RoundTo4Directions(Direction, Orientation)
```csharp
public Direction RoundTo4Directions(Direction direction, Orientation bias)
```
Rounds a diagonal direction to the nearest cardinal direction, using `bias` to break ties.

**Parameters** \
`direction` [Direction](../../Murder/Helpers/Direction.html) \
`bias` [Orientation](../../Murder/Core/Orientation.html) \

**Returns** \
[Direction](../../Murder/Helpers/Direction.html) \

#### ToAngle(Direction)
```csharp
public float ToAngle(Direction direction)
```

The angle of the direction, in radians.

**Parameters** \
`direction` [Direction](../../Murder/Helpers/Direction.html) \
\

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
\

#### GetFlipped(Direction)
```csharp
public ImageFlip GetFlipped(Direction direction)
```
Returns the `ImageFlip` flags needed to orient a sprite for the given direction.

**Parameters** \
`direction` [Direction](../../Murder/Helpers/Direction.html) \

**Returns** \
[ImageFlip](../../Murder/Core/Graphics/ImageFlip.html) \

#### GetFlippedHorizontal(Direction)
```csharp
public ImageFlip GetFlippedHorizontal(Direction direction)
```
Returns only the horizontal component of `ImageFlip` for the given direction.

**Parameters** \
`direction` [Direction](../../Murder/Helpers/Direction.html) \

**Returns** \
[ImageFlip](../../Murder/Core/Graphics/ImageFlip.html) \

#### ToCardinal(Direction, string, string, string, string)
```csharp
public string ToCardinal(Direction direction, string n, string e, string s, string w)
```
Maps a direction to one of the four provided cardinal label strings (N/E/S/W).

**Parameters** \
`direction` [Direction](../../Murder/Helpers/Direction.html) \
`n` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`e` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`s` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`w` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### ToCardinal(Direction)
```csharp
public string ToCardinal(Direction direction)
```
Returns the short compass string for the direction (e.g. `"N"`, `"SE"`).

**Parameters** \
`direction` [Direction](../../Murder/Helpers/Direction.html) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### ToCardinal4(Direction, string, string, string, bool)
```csharp
public string ToCardinal4(Direction direction, string n, string e, string s, bool verticalPriority)
```
Maps a direction to one of three cardinal label strings using four-direction snapping; `verticalPriority` determines tie-breaking for diagonal inputs.

**Parameters** \
`direction` [Direction](../../Murder/Helpers/Direction.html) \
`n` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`e` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`s` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`verticalPriority` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### GetName(int, int, bool)
```csharp
public ValueTuple<T1, T2> GetName(int i, int totalDirections, bool flipWest)
```
Returns the animation suffix name and flip flag for direction index `i` out of `totalDirections`.

**Parameters** \
`i` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`totalDirections` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`flipWest` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[ValueTuple\<T1, T2\>](https://learn.microsoft.com/en-us/dotnet/api/System.ValueTuple-2?view=net-7.0) \

#### GetSuffixFromAngle(Entity, AgentSpriteComponent, float)
```csharp
public ValueTuple<T1, T2> GetSuffixFromAngle(Entity entity, AgentSpriteComponent _, float angle)
```

Get the suffix from a suffix list based on an angle

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`_` [AgentSpriteComponent](../../Murder/Components/AgentSpriteComponent.html) \
`angle` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[ValueTuple\<T1, T2\>](https://learn.microsoft.com/en-us/dotnet/api/System.ValueTuple-2?view=net-7.0) \

#### ToCardinalFlipped(Direction, string, string, string)
```csharp
public ValueTuple<T1, T2> ToCardinalFlipped(Direction direction, string n, string e, string s)
```
Returns the animation suffix name and horizontal flip flag for the given direction using three cardinal label strings.

**Parameters** \
`direction` [Direction](../../Murder/Helpers/Direction.html) \
`n` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`e` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`s` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[ValueTuple\<T1, T2\>](https://learn.microsoft.com/en-us/dotnet/api/System.ValueTuple-2?view=net-7.0) \

#### ToCardinalFlipped(Direction)
```csharp
public ValueTuple<T1, T2> ToCardinalFlipped(Direction direction)
```

**Parameters** \
`direction` [Direction](../../Murder/Helpers/Direction.html) \

**Returns** \
[ValueTuple\<T1, T2\>](https://learn.microsoft.com/en-us/dotnet/api/System.ValueTuple-2?view=net-7.0) \

#### ToVector(Direction)
```csharp
public Vector2 ToVector(Direction direction)
```

**Parameters** \
`direction` [Direction](../../Murder/Helpers/Direction.html) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \



⚡
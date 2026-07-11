# Anchor

**Namespace:** Murder.Core.Cutscenes \
**Assembly:** Murder.dll

```csharp
public sealed struct Anchor
```

A named 2D world-space position used to place entities and camera targets during cutscenes.

**Intent:** Immutable position value that designates a specific point in the world for cutscene staging or entity spawning.

**Use-case:** Reference an `Anchor` on a cutscene entity to set where actors should move to or where the camera should focus during a scripted sequence.

### ⭐ Constructors
```csharp
public Anchor()
```

Creates an `Anchor` at position `Vector2.Zero`.

```csharp
public Anchor(Vector2 position)
```

Creates an `Anchor` at the specified world-space `position`.

**Parameters** \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

### ⭐ Properties
#### Position
```csharp
public readonly Vector2 Position;
```

The world-space position of this anchor point.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
### ⭐ Methods
#### WithPosition(Vector2)
```csharp
public Anchor WithPosition(Vector2 position)
```

Returns a copy of this anchor with `Position` replaced by the given `position`.

**Parameters** \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Anchor](../../../Murder/Core/Cutscenes/Anchor.html) \



⚡
# RoomComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct RoomComponent : IComponent
```

Marks a grid entity as a room: a rectangular section of the tile grid that has its own floor visual and camera behavior.

**Intent:** Mark a tile-grid entity as a discrete room and specify the floor visual asset used for it.

**Use-case:** Attach alongside [TileGridComponent](../../Murder/Components/TileGridComponent.html) on each room entity in a dungeon-style level — every entity with a `TileGridComponent` must also have a `RoomComponent`, enforced by the `[Requires]` attribute. `MapInitializerSystem` reads it while baking the tile grid into a [Map](../../Murder/Core/Map.html) to know which [FloorAsset](../../Murder/Assets/Graphics/FloorAsset.html) to paint under the room's tiles, and the level editor's tile-grid tools read/write it when authoring rooms. Set `Floor` to the desired floor tileset asset and `Flags` to configure camera behaviour, e.g. clamping the camera to the room's bounds.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public RoomComponent()
```

Creates a room with no floor asset assigned and no flags set.

```csharp
public RoomComponent(Guid floor)
```

Creates a room that renders `floor` as its floor asset, with no flags set.

**Parameters** \
`floor` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

### ⭐ Properties

#### Floor

```csharp
public readonly Guid Floor;
```

GUID of the [FloorAsset](../../Murder/Assets/Graphics/FloorAsset.html) used to render the floor underneath this room's tiles. `Guid.Empty` means no floor asset is assigned.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### Flags

```csharp
public readonly RoomFlags Flags;
```

Additional behavior flags for this room, e.g. `RoomFlags.ClampCamera` to keep the camera from scrolling outside the room's bounds.

**Returns** \
`RoomFlags` \

⚡

# RoomComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct RoomComponent : IComponent
```

This describes a room component properties.

**Intent:** Mark a tile-grid entity as a discrete room and specify the floor visual asset used for it.

**Use-case:** Attach alongside [TileGridComponent](../../Murder/Components/TileGridComponent.html) on each room entity in a dungeon-style level; set `Floor` to the desired floor tileset asset and `Flags` to configure camera behaviour.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public RoomComponent()
```

```csharp
public RoomComponent(Guid floor)
```

**Parameters** \
`floor` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

### ⭐ Properties
#### Floor
```csharp
public readonly Guid Floor;
```

GUID of the [FloorAsset](../../Murder/Assets/Graphics/FloorAsset.html) used to render the floor of this room.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \


⚡
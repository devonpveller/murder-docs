# TilesetComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct TilesetComponent : IComponent
```

Lists the tileset assets available for rendering tiles in the current world.

**Intent:** Tell the floor/tilemap render systems which [TilesetAsset](../../Murder/Assets/Graphics/TilesetAsset.html) assets are available to draw tile visuals from. Marked `[Unique]`, so a world is expected to carry at most one of these.

**Use-case:** Add once per world and populate `Tilesets` with the GUIDs of the [TilesetAsset](../../Murder/Assets/Graphics/TilesetAsset.html) files that define the tile visuals; the tilemap render systems look this component up to resolve which tileset to draw from when rendering a room's [TileGridComponent](../../Murder/Components/TileGridComponent.html).

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public TilesetComponent()
```

Creates a component with an empty tileset list.

```csharp
public TilesetComponent(ImmutableArray<T> tilesets)
```

Creates a component listing the given tileset asset GUIDs.

**Parameters** \
`tilesets` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

### ⭐ Properties

#### Tilesets

```csharp
public readonly ImmutableArray<T> Tilesets;
```

GUIDs of the [TilesetAsset](../../Murder/Assets/Graphics/TilesetAsset.html) assets available for rendering tiles in this world.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

### ⭐ Methods

#### WithTile(Guid)

```csharp
public TilesetComponent WithTile(Guid tile)
```

Returns a new component with the given tileset GUID appended to `Tilesets`.

**Parameters** \
`tile` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[TilesetComponent](../../Murder/Components/TilesetComponent.html) \

#### WithTiles(ImmutableArray<T>)

```csharp
public TilesetComponent WithTiles(ImmutableArray<T> tiles)
```

Returns a new component with `Tilesets` replaced entirely by the provided array.

**Parameters** \
`tiles` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

**Returns** \
[TilesetComponent](../../Murder/Components/TilesetComponent.html) \

⚡

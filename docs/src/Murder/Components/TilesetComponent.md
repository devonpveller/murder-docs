# TilesetComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct TilesetComponent : IComponent
```

This is a struct that points to a singleton class.
            Reactive systems won't be able to subscribe to this component.

**Intent:** Specify which tileset assets are used to render tiles in the current world.

**Use-case:** Add once per world (or room) entity and populate `Tilesets` with the GUIDs of the [TilesetAsset](../../Murder/Assets/Graphics/TilesetAsset.html) files that define the tile visuals.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public TilesetComponent()
```

```csharp
public TilesetComponent(ImmutableArray<T> tilesets)
```

**Parameters** \
`tilesets` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

### ⭐ Properties
#### Tilesets
```csharp
public readonly ImmutableArray<T> Tilesets;
```

List of GUIDs referencing the tileset assets available for rendering tiles in this entity's grid.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
### ⭐ Methods
#### WithTile(Guid)
```csharp
public TilesetComponent WithTile(Guid tile)
```

Returns a new component with the given tileset GUID appended to the list.

**Parameters** \
`tile` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[TilesetComponent](../../Murder/Components/TilesetComponent.html) \

#### WithTiles(ImmutableArray<T>)
```csharp
public TilesetComponent WithTiles(ImmutableArray<T> tiles)
```

Returns a new component with the tileset list replaced by the provided array.

**Parameters** \
`tiles` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

**Returns** \
[TilesetComponent](../../Murder/Components/TilesetComponent.html) \



⚡
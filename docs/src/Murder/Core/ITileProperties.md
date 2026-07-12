# ITileProperties

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public interface ITileProperties
```

Empty marker interface implemented by game-specific data types that describe extra, per-tileset or per-floor gameplay properties.

**Intent:** Murder itself never defines a concrete implementation of this interface — it exists purely as an extension point. A game project declares its own type implementing `ITileProperties` (e.g. `enum` or a small `struct`/`class` describing things like "is this floor icy?" or "does this tileset play a footstep sound?") and assigns an instance to `TilesetAsset.Properties` or `FloorAsset.Properties` in the editor.

**Use-case:** Systems that build the `Map` from tileset/floor assets (see `MapInitializerSystem.InitializeTile`) receive the configured `ITileProperties?` value back for each tile being processed and can cast or pattern-match it to the game's concrete type to apply game-specific behavior while rasterizing that tile into the `Map`. `TilesetAsset.GetProperties<T>()` provides a typed accessor (`where T : notnull, ITileProperties`) so call sites don't need to repeat the cast.

⚡

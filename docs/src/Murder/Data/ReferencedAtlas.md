# ReferencedAtlas

**Namespace:** Murder.Data \
**Assembly:** Murder.dll

```csharp
public sealed struct ReferencedAtlas
```

A single entry in a `WorldAsset.ReferencedAtlas` list: an atlas name (chosen via the `[AtlasName]` editor field) plus whether it should be unloaded when the owning world is torn down.

**Intent:** Lets a world declare, up front, which texture atlases its content needs so the engine can eagerly preload their textures the moment the world loads instead of stalling on first draw, and lets the world opt individual atlases into being freed automatically when it unloads (rather than persisting them for the rest of the game's lifetime).

**Use-case:** `GameScene.LoadContentImpl` iterates `WorldAsset.ReferencedAtlas` and calls `Game.Data.FetchAtlas(atlas.Id).LoadTextures()` for every entry right after the world is constructed. `GameScene.UnloadAsyncImpl` later iterates the same list and calls `Game.Data.DisposeAtlas(atlas.Id)` only for entries where `UnloadOnExit` is `true`, skipping atlases meant to stay resident (e.g. the static or gameplay atlas shared by every scene). Configure this list from the world editor rather than constructing `ReferencedAtlas` values by hand at runtime.

### ⭐ Constructors

```csharp
public ReferencedAtlas()
```

Parameterless constructor required for struct/editor serialization; produces an entry with an empty `Id` and `UnloadOnExit` set to `false`.

```csharp
public ReferencedAtlas(string id, bool unloadOnExit)
```

Creates a reference to the atlas named `id`, optionally marking it to be disposed when the owning world unloads.

**Parameters** \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`unloadOnExit` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

### ⭐ Properties

#### Id

```csharp
public readonly string Id;
```

Name of the referenced atlas (e.g. `"atlas"`, `"editor"`), matching one of the `AtlasIdentifiers` constants or a custom atlas filename. Passed directly to `GameDataManager.FetchAtlas`/`DisposeAtlas`. Decorated with `[AtlasName]` so the editor renders it as a dropdown of known atlas names instead of a free-text field.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### UnloadOnExit

```csharp
public readonly bool UnloadOnExit;
```

When `true`, `GameScene` disposes this atlas as soon as the owning world unloads, freeing its GPU memory. When `false`, the atlas is left loaded (useful for atlases shared across many worlds, so they aren't repeatedly reloaded on every scene transition).

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

⚡

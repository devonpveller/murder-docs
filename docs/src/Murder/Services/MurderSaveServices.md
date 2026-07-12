# MurderSaveServices

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public static class MurderSaveServices
```

Helpers for accessing the active save, applying dialogue/blackboard actions to it, and recording world-entity removal into it.

**Intent:** Provides a uniform API for creating or retrieving the active `SaveData`, executing `DialogAction`s (as produced by dialogue/interaction scripts) against a `BlackboardTracker`, and marking a world entity as permanently removed in the persistent save state.

**Use-case:** Call `CreateOrGetSave` to safely access save data from any system (creating one on demand rather than crashing if none exists yet), `DoAction` to mutate blackboard variables as part of dialogue or interaction logic, and `RecordAndMaybeDestroy` whenever gameplay code permanently removes an entity from the world so that the removal persists across a save/load.

### ⭐ Methods

#### CreateOrGetSave()

```csharp
public static SaveData CreateOrGetSave()
```

Returns the active `SaveData` (`Game.Data.TryGetActiveSaveData()`), creating a brand-new save via `Game.Data.CreateSave()` if none is currently active. Use this instead of `TryGetSave` whenever the calling code needs save data to exist unconditionally (for example, systems that record world state as the player plays).

**Returns** \
[SaveData](../../Murder/Assets/SaveData.html) \

#### DoAction(DialogAction)

```csharp
public static void DoAction(DialogAction action)
```

Applies `action` to the `BlackboardTracker` of the currently active save (creating a save first via `CreateOrGetSave` if needed). Convenience overload of `DoAction(BlackboardTracker, DialogAction)` for callers that don't already have a tracker reference on hand.

**Parameters** \
`action` [DialogAction](../../Murder/Core/Dialogs/DialogAction.html) \

#### DoAction(BlackboardTracker, DialogAction)

```csharp
public static void DoAction(BlackboardTracker tracker, DialogAction action)
```

Applies a `DialogAction` — a bool, int, float, or string assignment targeting a specific `Fact` — to `tracker`, dispatching to `SetBool`/`SetInt`/`SetFloat`/`SetString` based on `action.Fact.Kind`. This is the primitive that dialogue scripts and interaction systems use to mutate blackboard state (quest flags, counters, etc.) as the player progresses.

**Parameters** \
`tracker` [BlackboardTracker](../../Murder/Save/BlackboardTracker.html) \
`action` [DialogAction](../../Murder/Core/Dialogs/DialogAction.html) \

#### LoadSaveAndFetchTargetWorld(int)

```csharp
public static Guid? LoadSaveAndFetchTargetWorld(int slot)
```

Loads the save in `slot` as the active save (via `Game.Data.LoadSaveAsCurrentSave`) and returns the `Guid` of the world it was last saved in (`SaveData.CurrentWorld`), or `null` if loading failed. Used by the game's load-save flow to know which `WorldAsset` to transition into after a save file is loaded.

**Parameters** \
`slot` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[Guid?](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### RecordAndMaybeDestroy(Entity, World, bool)

```csharp
public static void RecordAndMaybeDestroy(this Entity entity, World world, bool destroy)
```

Records `entity` as removed from `world` in the active save (`SaveData.RecordRemovedEntityFromWorld`), so that reloading the world will not re-spawn it; optionally also calls `entity.Destroy()` immediately. Call this — rather than destroying an entity directly — for world content that should stay gone permanently once removed (e.g. a picked-up item, a defeated one-time enemy).

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`world` [World](../../Bang/World.html) \
`destroy` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TryGetSave()

```csharp
public static SaveData? TryGetSave()
```

Returns the active `SaveData`, or `null` if no save is currently loaded. Use this (instead of `CreateOrGetSave`) when the caller needs to distinguish "no save yet" from "a save exists" without the side effect of creating one.

**Returns** \
[SaveData?](../../Murder/Assets/SaveData.html) \

⚡

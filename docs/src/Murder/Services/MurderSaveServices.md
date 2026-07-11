# MurderSaveServices

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public static class MurderSaveServices
```

Helpers for accessing, modifying, and loading game save data.

**Intent:** Provides a uniform API for creating or retrieving the active save, executing blackboard actions, and managing the entity-to-save record relationship.

**Use-case:** Call `CreateOrGetSave` to safely access save data from any system, `DoAction` to mutate blackboard variables as part of dialogue or interaction logic, and `RecordAndMaybeDestroy` to mark a world entity as removed in the persistent save state.

### ⭐ Methods
#### CreateOrGetSave()
```csharp
public SaveData CreateOrGetSave()
```
Returns the active `SaveData`, creating a new one if no active save exists.

**Returns** \
[SaveData](../../Murder/Assets/SaveData.html) \

#### TryGetSave()
```csharp
public SaveData TryGetSave()
```
Returns the active `SaveData`, or `null` if no save is currently loaded.

**Returns** \
[SaveData](../../Murder/Assets/SaveData.html) \

#### LoadSaveAndFetchTargetWorld(int)
```csharp
public T? LoadSaveAndFetchTargetWorld(int slot)
```
Loads the save in `slot` as the active save and returns the `Guid` of the world it was last saved in.

**Parameters** \
`slot` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### DoAction(BlackboardTracker, DialogAction)
```csharp
public void DoAction(BlackboardTracker tracker, DialogAction action)
```
Applies a `DialogAction` (bool, int, float, or string assignment) to the provided `BlackboardTracker`.

**Parameters** \
`tracker` [BlackboardTracker](../../Murder/Save/BlackboardTracker.html) \
`action` [DialogAction](../../Murder/Core/Dialogs/DialogAction.html) \

#### RecordAndMaybeDestroy(Entity, World, bool)
```csharp
public void RecordAndMaybeDestroy(Entity entity, World world, bool destroy)
```
Records the entity as removed from the world in the active save; optionally destroys the entity immediately.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`world` [World](../../Bang/World.html) \
`destroy` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \



⚡
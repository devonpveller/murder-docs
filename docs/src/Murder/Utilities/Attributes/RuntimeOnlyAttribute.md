# RuntimeOnlyAttribute

**Namespace:** Murder.Utilities.Attributes \
**Assembly:** Murder.dll

```csharp
public class RuntimeOnlyAttribute : Attribute
```

Marks a component type as runtime-only: it is never part of a saved world/asset and is only ever added dynamically while the game is running.

**Intent:** Keeps derived/transient component state out of saved data and out of the editor's manual "Add Component" flow, since it wouldn't survive a reload anyway.

**Use-case:** Apply to components that hold state recomputed every session, such as pathfinding caches, per-frame signals, or singleton trackers that must always start fresh (e.g. `HAAStarPathfindComponent`, `PathfindStatusComponent`, `AnimationCompleteComponent`, `RuleWatcherComponent`). `SavedWorldBuilder` checks for this attribute and skips components carrying it when serializing the world for save games, and the editor's `AssetsFilter` excludes them from the "Add Component" list.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors

```csharp
public RuntimeOnlyAttribute()
```

### ⭐ Properties

#### TypeId

```csharp
public virtual Object TypeId { get; }
```

Unique object identity for this attribute type, inherited from `Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

⚡

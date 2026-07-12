# BlackboardTracker

**Namespace:** Murder.Save \
**Assembly:** Murder.dll

```csharp
public class BlackboardTracker
```

Track variables that contain the state of the world.

**Intent:** Provides the runtime read/write layer over all registered `IBlackboard` instances, enabling dialogue systems and game logic to query and modify named variables by string.

**Use-case:** Access via `Game.Save.BlackboardTracker` to get or set blackboard fields by name, check dialogue play counts, or evaluate `Criterion` conditions for branching dialogue.

### ⭐ Constructors

```csharp
public BlackboardTracker()
```

Creates a new empty tracker with no registered blackboards.

### ⭐ Methods

#### SetValue(BlackboardInfo, string, T, bool)

```csharp
protected bool SetValue(BlackboardInfo info, string fieldName, T value, bool isRevertingTrigger)
```

Sets the value of the named field on the blackboard described by `info`; returns `true` if the field was changed.

**Parameters** \
`info` [BlackboardInfo](../../Murder/Data/BlackboardInfo.html) \
`fieldName` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`value` [T](../../) \
`isRevertingTrigger` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### OnFieldModified(string, Guid?, FieldInfo, string, T)

```csharp
protected virtual void OnFieldModified(string blackboardName, Guid? blackboardGuid, FieldInfo fieldInfo, string fieldName, T value)
```

Extension point called by `SetValue` right after a field is successfully written (and after any `[Trigger]` bookkeeping), naming the blackboard (`blackboardName`/`blackboardGuid` for character-scoped ones), the reflected `fieldInfo`, `fieldName`, and the new `value`. The base implementation is empty — third-party/game code overrides it to react to specific value changes, e.g. to fire UI notifications or achievement checks.

**Parameters** \
`blackboardName` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`blackboardGuid` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`fieldInfo` [FieldInfo](https://learn.microsoft.com/en-us/dotnet/api/System.Reflection.FieldInfo?view=net-7.0) \
`fieldName` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`value` [T](../../) \

#### GetBool(string, string, T?)

```csharp
public bool GetBool(string name, string fieldName, T? character)
```

Returns the boolean value of the named field on the blackboard with the given name.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`fieldName` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`character` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HasPlayed(Guid, string, int)

```csharp
public bool HasPlayed(Guid guid, string situationId, int dialogId)
```

Returns whether a particular dialog option has been played, by checking whether `Track` has ever been called for the same `(guid, situationId, dialogId)` triple.

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`situationId` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`dialogId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HasVariable(string, string)

```csharp
public bool HasVariable(string blackboardName, string fieldName)
```

Return whether a <paramref name="fieldName" /> exists on <paramref name="blackboardName" />.

**Parameters** \
`blackboardName` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`fieldName` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Matches(Criterion, T?, World, T?, out Int32&)

```csharp
public bool Matches(Criterion criterion, T? character, World world, T? entityId, Int32& weight)
```

Evaluates a dialogue `Criterion` against the current blackboard state; returns `true` if the criterion is satisfied and writes the match weight to `weight`.

**Parameters** \
`criterion` [Criterion](../../Murder/Core/Dialogs/Criterion.html) \
`character` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`world` [World](../../Bang/World.html) \
`entityId` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`weight` [int&](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### SetValueForAllCharacterBlackboards(string, string, T)

```csharp
public bool SetValueForAllCharacterBlackboards(string blackboardName, string fieldName, T value)
```

Sets `fieldName` to `value` on the blackboard named `blackboardName` for every character that already has a cached character-scoped blackboard set (see `FindBlackboard`/`FetchCharacterFor`). Stops early and returns `false` the moment one of those characters turns out not to have a `blackboardName` blackboard at all; returns `true` only if every already-tracked character had it and got updated. Characters that have not yet had their blackboards initialized (i.e. this speaker was never looked up before) are not touched.

**Parameters** \
`blackboardName` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`fieldName` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`value` [T](../../) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### GetFloat(string, string, T?)

```csharp
public float GetFloat(string name, string fieldName, T? character)
```

Returns the float value of the named field on the blackboard with the given name.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`fieldName` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`character` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### GetInt(string, string, T?)

```csharp
public int GetInt(string name, string fieldName, T? character)
```

Returns the integer value of the named field on the blackboard with the given name.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`fieldName` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`character` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### PlayCount(Guid, string, int)

```csharp
public int PlayCount(Guid guid, string situationId, int dialogId)
```

Returns how many times the dialog option identified by `(guid, situationId, dialogId)` has been played (0 if it has never been tracked). Dialogue scripts use this to branch on repeat visits — e.g. showing a different line the second time a topic is picked.

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`situationId` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`dialogId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### GetString(string, string, T?)

```csharp
public string GetString(string name, string fieldName, T? character)
```

Returns the string value of the named field on the blackboard with the given name.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`fieldName` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`character` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### GetValueAsString(string)

```csharp
public string? GetValueAsString(string fieldName)
```

Scans every registered blackboard (not just a single named one) for a field called `fieldName` and returns its value formatted as a string, or `null` if no blackboard defines that field. If the field's raw value is itself a `string`, it is first run through `ValidateStringField` so language-specific validation/formatting can apply.

**Parameters** \
`fieldName` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### FetchCharacterFor(Guid)

```csharp
public T? FetchCharacterFor(Guid guid)
```

Fetch a cached character out of [BlackboardTracker.\_characterCache](../../Murder/Save/BlackboardTracker.html#_charactercache)

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
\

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
\

#### FindBlackboard(string, T?)

```csharp
public virtual BlackboardInfo FindBlackboard(string name, T? guid)
```

Locates and returns the `BlackboardInfo` for the blackboard with the given name, optionally scoped to a character GUID.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`guid` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

**Returns** \
[BlackboardInfo](../../Murder/Data/BlackboardInfo.html) \

#### FetchBlackboards()

```csharp
public virtual ImmutableDictionary<TKey, TValue> FetchBlackboards()
```

Returns an immutable map of all registered blackboard names to their `BlackboardInfo` descriptors.

**Returns** \
[ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

#### Track(Guid, string, int)

```csharp
public virtual void Track(Guid character, string situationId, int dialogId)
```

Records that the dialog option `dialogId` inside `situationId` of the character `character` has just been played, incrementing its play count by one. Called by the dialogue system every time a line or choice is consumed, so that later `HasPlayed`/`PlayCount` checks (and criteria that depend on them) reflect the player's history.

**Parameters** \
`character` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`situationId` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`dialogId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### OnModified(BlackboardKind)

```csharp
public void OnModified(BlackboardKind kind)
```

Notify that the blackboard has been changed (externally or internally).

**Parameters** \
`kind` [BlackboardKind](../../Murder/Core/Dialogs/BlackboardKind.html) \

#### ResetAllWatchers(Action, BlackboardKind[])

```csharp
public void ResetAllWatchers(Action notification, BlackboardKind[] kinds)
```

Convenience wrapper around `ResetWatcher` that unsubscribes `notification` from every `BlackboardKind` in `kinds` in one call.

**Parameters** \
`notification` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \
`kinds` [BlackboardKind[]](../../Murder/Core/Dialogs/BlackboardKind.html) \

#### ResetPendingTriggers()

```csharp
public void ResetPendingTriggers()
```

Reset all fields marked with a [Trigger] attribute, so they are only activated for one frame.

#### ResetWatcher(BlackboardKind, Action)

```csharp
public void ResetWatcher(BlackboardKind kind, Action notification)
```

This will reset all watchers of trackers.

**Parameters** \
`kind` [BlackboardKind](../../Murder/Core/Dialogs/BlackboardKind.html) \
`notification` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \

#### SetBool(string, string, BlackboardActionKind, bool, T?)

```csharp
public void SetBool(string name, string fieldName, BlackboardActionKind kind, bool value, T? character)
```

Sets the boolean `fieldName` on the named blackboard using the specified `BlackboardActionKind` operation.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`fieldName` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`kind` [BlackboardActionKind](../../Murder/Core/Dialogs/BlackboardActionKind.html) \
`value` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`character` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### SetFloat(string, string, BlackboardActionKind, float, T?)

```csharp
public void SetFloat(string name, string fieldName, BlackboardActionKind kind, float value, T? character)
```

Sets the float `fieldName` on the named blackboard using the specified `BlackboardActionKind` operation.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`fieldName` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`kind` [BlackboardActionKind](../../Murder/Core/Dialogs/BlackboardActionKind.html) \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`character` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### SetInt(string, string, BlackboardActionKind, int, T?)

```csharp
public void SetInt(string name, string fieldName, BlackboardActionKind kind, int value, T? character)
```

Sets the integer `fieldName` on the named blackboard using the specified `BlackboardActionKind` operation.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`fieldName` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`kind` [BlackboardActionKind](../../Murder/Core/Dialogs/BlackboardActionKind.html) \
`value` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`character` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### SetString(string, string, string, T?)

```csharp
public void SetString(string name, string fieldName, string value, T? character)
```

Assigns `value` to the string field `fieldName` on blackboard `name` (optionally scoped to `character`). Unlike the numeric setters there is no `BlackboardActionKind` overload — strings are always a direct set. Does nothing if the blackboard cannot be found.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`fieldName` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`value` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`character` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### GetValue(string, string, T?)

```csharp
public T? GetValue(string name, string fieldName, T? character)
```

Generic escape hatch for reading a blackboard field whose type is not `bool`/`int`/`float`/`string` (e.g. an enum fact), such as those consumed by `Matches` when evaluating a `Criterion`. Returns `default` if the blackboard cannot be found; prefer the typed `GetBool`/`GetInt`/`GetFloat`/`GetString` when the field's type is already known.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`fieldName` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`character` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### SetValue(string, string, T, T?)

```csharp
public void SetValue(string name, string fieldName, T value, T? character)
```

Generic escape hatch for writing a blackboard field of any type, mirroring `GetValue(string, string, T?)`. Does nothing if `name` does not resolve to a known blackboard.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`fieldName` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`value` [T](../../) \
`character` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### Watch(Action, BlackboardKind)

```csharp
public void Watch(Action notification, BlackboardKind kind)
```

This will watch any chages to any of the blackboard properties.

**Parameters** \
`notification` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \
`kind` [BlackboardKind](../../Murder/Core/Dialogs/BlackboardKind.html) \

#### WatchAll(Action, BlackboardKind[])

```csharp
public void WatchAll(Action notification, BlackboardKind[] kinds)
```

Convenience wrapper around `Watch` that subscribes `notification` to every `BlackboardKind` in `kinds` in one call.

**Parameters** \
`notification` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \
`kinds` [BlackboardKind[]](../../Murder/Core/Dialogs/BlackboardKind.html) \

⚡

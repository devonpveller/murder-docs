# BlackboardInfo

**Namespace:** Murder.Data \
**Assembly:** Murder.dll

```csharp
public class BlackboardInfo
```

Bundles a resolved blackboard together with the metadata `BlackboardTracker` needs to look it up and read/write its fields via reflection: its declared name, an optional owning character GUID, its CLR `Type`, and the live `IBlackboard` instance itself.

**Intent:** `BlackboardTracker` discovers every `[Blackboard]`-tagged class in the loaded assemblies at startup (see `BlackboardTracker.InitializeBlackboards`/`InitializeCharacterBlackboards`), instantiates one of each, and wraps the instance in a `BlackboardInfo` so it can be indexed by name (and, for character-scoped blackboards, by character GUID) without losing the concrete `Type` needed for `FieldInfo` lookups.

**Use-case:** Returned by `BlackboardTracker.FindBlackboard(name, guid)` and consumed internally by `BlackboardTracker`'s `GetBool`/`SetBool`/`GetInt`/`SetInt`/`GetFloat`/`SetFloat`/`GetString`/`SetString`/`GetValue<T>`/`SetValue<T>`/`Matches` methods, which use `Type.GetField` against `BlackboardInfo.Type` and then read/write the field on `BlackboardInfo.Blackboard`. Game code and dialogue scripts almost never construct a `BlackboardInfo` directly — it is produced by the tracker's blackboard discovery pass.

### ⭐ Constructors

```csharp
public BlackboardInfo(string name, Guid? guid, Type type, IBlackboard blackboard)
```

Creates a new `BlackboardInfo` pairing a blackboard instance with the lookup metadata `BlackboardTracker` needs: the name it is registered under, the character GUID that owns it (or `null` for a global/default blackboard), its CLR type, and the instance itself.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`guid` [Guid?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`type` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
`blackboard` [IBlackboard](../../Murder/Core/Dialogs/IBlackboard.html) \

### ⭐ Properties

#### Name

```csharp
public readonly string Name;
```

The blackboard's registered name, taken from `BlackboardAttribute.Name` at discovery time. This is the string dialogue scripts and `BlackboardTracker.FindBlackboard` use to address the blackboard (e.g. as `criterion.Fact.Blackboard`).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Guid

```csharp
public readonly Guid? Guid;
```

The GUID of the character script this blackboard belongs to, or `null` when the blackboard is a global/default blackboard rather than a per-character one. Used to disambiguate character-scoped blackboards that share the same declared name across different characters.

**Returns** \
[Guid?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### Type

```csharp
public readonly Type Type;
```

The CLR type of the blackboard class. `BlackboardTracker` uses this with reflection (`Type.GetField`) to locate and read/write individual fact fields on `Blackboard` by name, since the tracker only knows field names as strings coming from dialogue data.

**Returns** \
[Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

#### Blackboard

```csharp
public readonly IBlackboard Blackboard;
```

The live blackboard instance whose fields actually hold the tracked values. This is the object reflection reads from and writes to; its concrete type matches `Type`.

**Returns** \
[IBlackboard](../../Murder/Core/Dialogs/IBlackboard.html) \

⚡

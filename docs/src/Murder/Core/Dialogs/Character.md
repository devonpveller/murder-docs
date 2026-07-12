# Character

**Namespace:** Murder.Core.Dialogs \
**Assembly:** Murder.dll

```csharp
public sealed struct Character
```

Immutable data record for a dialogue character asset, bundling the character's identity, default speaker, portrait, and all authored situations.

**Intent:** Represents the complete authored dialogue script for one character: who speaks, which portrait is shown by default, and the full set of `Situation`s that constitute their dialogue graph.

**Use-case:** Loaded from a `CharacterAsset` and handed to `CharacterRuntime` to drive a live dialogue session; read `Situations` to enumerate all authored dialogue trees for a character.

### ⭐ Constructors

```csharp
public Character(Guid guid, Guid speaker, string portrait, ImmutableDictionary<TKey, TValue> situations)
```

Creates a fully-initialised character record with the given asset GUID, speaker GUID, default portrait, and situation dictionary.

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`speaker` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`portrait` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`situations` [ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

### ⭐ Properties

#### Guid

```csharp
public readonly Guid Guid;
```

The guid of the character asset being tracked by this.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### Portrait

```csharp
public readonly string Portrait;
```

The default portrait for [Character.Speaker](../../../Murder/Core/Dialogs/Character.html#speaker). If null, use the speaker
default portrait.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Situations

```csharp
public readonly ImmutableDictionary<TKey, TValue> Situations;
```

All situations for the character, keyed by `Situation.Name`. Looked up by `CharacterRuntime.StartAtSituation` to select the active conversation state.

**Returns** \
[ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

#### Speaker

```csharp
public readonly Guid Speaker;
```

The speaker is the owner of this dialog. Used when a null
speaker is found.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

⚡

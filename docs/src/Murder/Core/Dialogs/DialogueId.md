# DialogueId

**Namespace:** Murder.Core.Dialogs \
**Assembly:** Murder.dll

```csharp
public sealed struct DialogueId : IEquatable<T>
```

This represents an item id in the dialog that has been manually modified by the user
and should be persisted.

**Intent:** Acts as a stable three-part key — situation name, dialog id, and item (line/action) index — identifying one specific line or action inside a character's dialogue asset, so per-line overrides (custom portraits, events, components, actions) survive re-imports of the dialogue script.

**Use-case:** `CharacterRuntime` builds a `DialogueId` for the line it is currently playing (from the active situation's name, dialog id, and line index) and looks it up in `CharacterAsset.Data` to find any `LineInfo` override authored for that line. The dialogue editor does the same when the user edits a line's portrait, event, or attached component so the change is recorded against a stable identity rather than a raw list index that would shift as the script is edited.

### ⭐ Constructors

```csharp
public DialogueId(string name, int dialog, int id)
```

Creates a key identifying the item at `id` inside the dialog `dialog`, within the situation named `name`.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`dialog` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties

#### DialogId

```csharp
public readonly int DialogId;
```

The `Dialog.Id` of the dialog node within the situation that contains this item.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### ItemId

```csharp
public readonly int ItemId;
```

The index of the specific item (a line, or an action) within the dialog node's line list.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### UniqueName

```csharp
public readonly string UniqueName;
```

The name of the `Situation` that owns this item, used as the first component of the key so the same dialog/item index in two different situations does not collide.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

⚡

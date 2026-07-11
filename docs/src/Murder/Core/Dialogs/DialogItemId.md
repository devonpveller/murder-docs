# DialogItemId

**Namespace:** Murder.Core.Dialogs \
**Assembly:** Murder.dll

```csharp
public sealed struct DialogItemId
```

This represents an item in the dialog that has been manually modified by the user
            and should be persisted.

**Intent:** Acts as a stable three-part key (situation + dialog + item) identifying a specific line or action within a character's dialogue asset, so user edits survive re-imports.

**Use-case:** Used by the editor when tracking overrides to individual dialog items; pass one to look up or update a specific element in the character's `Situations` hierarchy.

### ⭐ Constructors
```csharp
public DialogItemId(int situation, int dialog, int id)
```

Creates a key identifying the item at `id` inside `dialog` inside `situation`.

**Parameters** \
`situation` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`dialog` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties
#### DialogId
```csharp
public readonly int DialogId;
```

The index of the `Dialog` node within the `Situation` that contains this item.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### ItemId
```csharp
public readonly int ItemId;
```

The index of the specific item (line or action) within the `Dialog` node.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### SituationId
```csharp
public readonly int SituationId;
```

The index of the `Situation` within the character's situation list.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \


⚡
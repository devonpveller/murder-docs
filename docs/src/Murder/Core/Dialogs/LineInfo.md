# LineInfo

**Namespace:** Murder.Core.Dialogs \
**Assembly:** Murder.dll

```csharp
public sealed struct LineInfo
```

Per-line override data that a writer can attach to an individual dialogue line or action in the editor — a custom speaker/portrait, a sound event, a component to apply, an action to run before the line, and behavior flags.

**Intent:** Separates hand-authored, editor-only tweaks to a specific dialogue line from the line's own authored content (`Line`), so those tweaks survive a re-import/regeneration of the dialogue script text.

**Use-case:** Stored keyed by `DialogueId` on the owning `CharacterAsset` (via `DialogueLineInfo`); `CharacterAsset.SetCustomPortraitAt`, `SetEventInfoAt`, and `SetActionAt` create or update entries, and `CharacterRuntime`/the dialogue editor read `Data` to layer this override on top of the authored `Line` when the dialogue is played or edited.

### ⭐ Constructors

```csharp
public LineInfo()
```

Creates an empty override with no speaker, portrait, event, action, component, or flags set.

### ⭐ Properties

#### ActionBeforeLine

```csharp
public T? ActionBeforeLine { get; init; }
```

Optional action from this same line.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### Component

```csharp
public IComponent Component { get; init; }
```

Component modified within a dialog.

**Returns** \
[IComponent](../../../Bang/Components/IComponent.html) \

#### Empty

```csharp
public bool Empty { get; }
```

Returns `true` when none of the override fields (speaker, portrait, event, component) are set, meaning this entry carries no useful data and can be pruned.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Event

```csharp
public string Event { get; init; }
```

Overrides the custom sound event fired when this line plays; `null` means no custom event override.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Flags

```csharp
public LineInfoProperties Flags { get; init; }
```

Behavior overrides for this line; see [LineInfoProperties](../../../Murder/Core/Dialogs/LineInfoProperties.html).

**Returns** \
[LineInfoProperties](../../../Murder/Core/Dialogs/LineInfoProperties.html) \

#### Portrait

```csharp
public readonly string Portrait { get; init; }
```

Overrides the portrait key shown for this line; `null` means use the line's own/default portrait.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Speaker

```csharp
public readonly Guid Speaker { get; init; }
```

Overrides the speaking character for this line; `Guid.Empty` means use the line's own speaker.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

⚡

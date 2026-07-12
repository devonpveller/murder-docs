# DialogueEditorAttribute

**Namespace:** Murder.Attributes \
**Assembly:** Murder.dll

```csharp
public class DialogueEditorAttribute : Attribute
```

Marks an [ISystem](../../Bang/Systems/ISystem.html) as belonging to the dialogue/story editing tools, so it is only activated while a dialogue-related editor window is open.

**Intent:** Keep dialogue-editing-only systems (such as dialogue node visualization) out of the editor stage by default, and let dialogue-focused editor windows turn them on for the duration of that editing session.

**Use-case:** Apply to systems that only make sense while inspecting or authoring dialogue graphs, such as `DialogueNodeSystem`. `StageHelpers` registers systems carrying this attribute disabled by default alongside the other special-purpose editor modes (Tile Editor, Pathfind Editor, Sound Editor), and `CharacterEditor` explicitly calls `stage.ActivateSystemsWith(enable: true, typeof(DialogueEditorAttribute))` to enable them when the character/dialogue editor is opened.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors

```csharp
public DialogueEditorAttribute()
```

Creates a new instance of `DialogueEditorAttribute`.

### ⭐ Properties

#### TypeId

```csharp
public virtual Object TypeId { get; }
```

Unique type identifier for this attribute, inherited from `System.Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

⚡

# DefaultEditorSystemAttribute

**Namespace:** Murder.Attributes \
**Assembly:** Murder.dll

```csharp
public class DefaultEditorSystemAttribute : Attribute
```

Marks an [ISystem](../../Bang/Systems/ISystem.html) implementation so the Murder editor automatically registers it as an editor-only system, even though it wouldn't otherwise be part of the game's normal system list.

**Intent:** Let a system opt into running inside the editor stage (gizmos, debug overlays, preview-only listeners, etc.) without being wired into the game's regular world systems. `StageHelpers` scans all types for this attribute and adds each matching system to the editor.

**Use-case:** Apply to system classes that should only ever run in the editor. Use the default constructor (or `startActive: true`) for systems that should be active as soon as the editor loads, and `startActive: false` for systems that should be registered but left disabled until the user manually enables them from the editor's systems list — for example `EventListenerSystem` in `src/Murder/Systems/Effects/EventListenerSystem.cs` uses `[DefaultEditorSystem(startActive: false)]` on two of its listener systems so they can be toggled on only when needed. Combine with [IgnoreFromEditorAttribute](../../Murder/Attributes/IgnoreFromEditorAttribute.html) to skip a type entirely even if it carries this attribute.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors

```csharp
public DefaultEditorSystemAttribute()
```

Creates a new instance with `StartActive` set to `true`.

```csharp
public DefaultEditorSystemAttribute(bool startActive)
```

Creates a new instance specifying whether the system begins in the active state.

**Parameters** \
`startActive` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

### ⭐ Properties

#### StartActive

```csharp
public readonly bool StartActive;
```

Whether the system should begin in the active (enabled) state when the editor loads.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TypeId

```csharp
public virtual Object TypeId { get; }
```

Unique type identifier for this attribute, inherited from `System.Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

⚡

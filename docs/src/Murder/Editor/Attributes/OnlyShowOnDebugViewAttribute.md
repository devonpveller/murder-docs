# OnlyShowOnDebugViewAttribute

**Namespace:** Murder.Editor.Attributes \
**Assembly:** Murder.dll

```csharp
public class OnlyShowOnDebugViewAttribute : Attribute
```

Marks an `ISystem` class as belonging to the editor's debug-only overlay group, rather than running all the time.

**Intent:** Systems tagged with this attribute are discovered via reflection by `DebugActivatorSystem` at world startup and are kept deactivated until the developer toggles the debug view (by default, pressing F2 in the editor's play-test/stage view), at which point every tagged system is activated together, and deactivated again when the debug view is turned off.

**Use-case:** Apply this to systems that draw editor-only diagnostics -- collider outlines, pathfinding routes, sound ranges, entity selection gizmos, texture/shader inspectors and similar -- so they stay out of the way during normal play-testing and only appear when explicitly requested. This is a system-level toggle, not a per-component or per-property visibility flag; to hide individual inspector fields instead, use `HideInEditorAttribute`. Real examples in the engine include `DebugColliderRenderSystem`, `DebugRouteSystem`, `PhysicsDebugSystem`, `QuadTreeDebugSystem` and `EntitiesSelectorSystem`, all decorated with `[OnlyShowOnDebugView]`.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors

```csharp
public OnlyShowOnDebugViewAttribute()
```

Creates a new instance of the marker attribute. It carries no data -- its mere presence on a class is what `DebugActivatorSystem` looks for via reflection.

### ⭐ Properties

#### TypeId

```csharp
public virtual Object TypeId { get; }
```

Unique type identifier for this attribute, inherited from `System.Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

⚡

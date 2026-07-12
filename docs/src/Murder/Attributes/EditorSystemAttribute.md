# EditorSystemAttribute

**Namespace:** Murder.Attributes \
**Assembly:** Murder.dll

```csharp
public class EditorSystemAttribute : Attribute
```

Attribute for systems which will show up in the "Editor" mode.

**Intent:** Mark an [ISystem](../../Bang/Systems/ISystem.html) as an editor-mode system that is always registered and started active whenever the Murder editor stage is built.

**Use-case:** Apply to systems that must always run while editing — unlike [DefaultEditorSystemAttribute](../../Murder/Attributes/DefaultEditorSystemAttribute.html) (where each system can opt to start disabled), every system found with `[EditorSystem]` is unconditionally enabled by `StageHelpers`. Many built-in render and debug systems use it this way, including `RectangleRenderSystem`, `PolygonSpriteRenderSystem`, the particle render/tracker systems, `CursorSystem`, and `EditorCameraControllerSystem`, so their visuals and interactions stay active throughout an editing session even though the same systems also ship in the game.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors

```csharp
public EditorSystemAttribute()
```

Creates a new instance of `EditorSystemAttribute`.

### ⭐ Properties

#### TypeId

```csharp
public virtual Object TypeId { get; }
```

Unique type identifier for this attribute, inherited from `System.Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

⚡

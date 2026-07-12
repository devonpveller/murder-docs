# CutsceneAnchorsEditorComponent

**Namespace:** Murder.Components.Serialization \
**Assembly:** Murder.dll

```csharp
public sealed struct CutsceneAnchorsEditorComponent : IComponent
```

Editor-authored collection of named anchor points ("marks") for a cutscene entity, e.g. camera targets or positions characters should walk to.

**Implements:** _[IComponent](../../../Bang/Components/IComponent.html)_

**Intent:** This is the component the level/cutscene editor reads and writes (via [AddAnchorAt](#addanchoratvector2), [WithAnchorAt](#withanchoratstring-vector2), [WithoutAnchorAt](#withoutanchoratstring)) while a cutscene is being designed. At world-load time, `WorldProcessor` consumes this component, converts [Anchors](#anchors) into an efficient name-to-position dictionary on a runtime [CutsceneAnchorsComponent](../../../Murder/Components/Cutscenes/CutsceneAnchorsComponent.html), and removes this component from the entity — so it should only ever be present on entities before the world finishes loading, not during actual gameplay.

**Use-case:** Add to an entity that acts as a cutscene container; populate `Anchors` with one [AnchorId](../../../Murder/Components/Serialization/AnchorId.html) per named mark, then reference those names in cutscene scripts or through the cutscene editor's anchor tools.

### ⭐ Constructors

```csharp
public CutsceneAnchorsEditorComponent()
```

Default constructor; `Anchors` starts as an empty list.

```csharp
public CutsceneAnchorsEditorComponent(ImmutableArray<T> anchors)
```

Creates the component pre-populated with the given list of named anchors.

**Parameters** \
`anchors` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) — the named anchors to store. \

### ⭐ Properties

#### Anchors

```csharp
public readonly ImmutableArray<T> Anchors;
```

The ordered list of named anchors authored for this cutscene entity.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

### ⭐ Methods

#### FindAnchor(string)

```csharp
public Anchor FindAnchor(string name)
```

Looks up the anchor named `name` (exact, case-sensitive match) and returns its [Anchor](../../../Murder/Core/Cutscenes/Anchor.html), or a default anchor if not found.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[Anchor](../../../Murder/Core/Cutscenes/Anchor.html) \

#### AddAnchorAt(Vector2)

```csharp
public CutsceneAnchorsEditorComponent AddAnchorAt(Vector2 newPosition)
```

Creates and appends a new anchor at the given world-space position, automatically naming it with its zero-based index (as a string). Used by the cutscene editor when a designer creates a new anchor mark.

**Parameters** \
`newPosition` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[CutsceneAnchorsEditorComponent](../../../Murder/Components/Serialization/CutsceneAnchorsEditorComponent.html) \

#### WithAnchorAt(string, Vector2)

```csharp
public CutsceneAnchorsEditorComponent WithAnchorAt(string name, Vector2 newPosition)
```

Returns a new component with the named anchor moved to `newPosition`; returns the same instance unchanged if no anchor with that name exists. `name` is matched case-insensitively. Used by the cutscene editor when a designer drags an anchor gizmo.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`newPosition` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[CutsceneAnchorsEditorComponent](../../../Murder/Components/Serialization/CutsceneAnchorsEditorComponent.html) \

#### WithoutAnchorAt(string)

```csharp
public CutsceneAnchorsEditorComponent WithoutAnchorAt(string name)
```

Returns a new component with the named anchor removed from the list; returns the same instance unchanged if no anchor with that name exists. `name` is matched case-insensitively. Used by the cutscene editor when a designer deletes an anchor.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[CutsceneAnchorsEditorComponent](../../../Murder/Components/Serialization/CutsceneAnchorsEditorComponent.html) \

⚡

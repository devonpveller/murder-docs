# Anchor

**Namespace:** Murder.Core.Cutscenes \
**Assembly:** Murder.dll

```csharp
public sealed struct Anchor
```

An immutable 2D world-space position, used as the payload of a named anchor point inside a cutscene's anchor collection (see `CutsceneAnchorsComponent` and the editor-only `CutsceneAnchorsEditorComponent`/`AnchorId`, which pair an `Anchor` with a string name).

**Intent:** Lightweight value type that designates a specific point in the world for cutscene staging, without carrying any identity of its own — the name/id lives in whichever collection stores the `Anchor`.

**Use-case:** Cutscene tooling authors a set of named anchors on an entity (e.g. "actor_spawn", "camera_focus"); at runtime, cutscene systems look up the `Anchor` by name and use its `Position` to place actors or aim the camera.

### ⭐ Constructors

```csharp
public Anchor()
```

Creates an `Anchor` at position `Vector2.Zero`.

```csharp
public Anchor(Vector2 position)
```

Creates an `Anchor` at the specified world-space `position`.

**Parameters** \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

### ⭐ Properties

#### Position

```csharp
public readonly Vector2 Position;
```

The world-space position of this anchor point.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

### ⭐ Methods

#### WithPosition(Vector2)

```csharp
public Anchor WithPosition(Vector2 position)
```

Returns a copy of this anchor with `Position` replaced by the given `position`.

**Parameters** \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Anchor](../../../Murder/Core/Cutscenes/Anchor.html) \

⚡

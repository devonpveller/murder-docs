# StageSetting

**Namespace:** Murder.Editor.Assets \
**Assembly:** Murder.dll

```csharp
[Flags]
public enum StageSetting : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Flags controlling which debug overlays are drawn on top of an editor stage.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

**Intent:** Lets the editor remember, per stage, which debug overlays (sound emitters, sprite bounds, colliders) the developer had toggled on. Combined via bitwise OR and stored in [PersistStageInfo.Settings](../../../Murder/Editor/Assets/PersistStageInfo.html#settings), which is itself persisted per-stage in [EditorSettingsAsset.StageInfo](../../../Murder/Editor/Assets/EditorSettingsAsset.html#stageinfo) so each scene remembers which overlays were on the last time it was open.

**Use-case:** Read by the editor's stage rendering code to decide whether to draw sound-emitter icons, sprite bounding boxes, and/or collider shapes on top of the scene. `ShowCollider` is the default value for a freshly created snapshot.

### ⭐ Properties

#### None

```csharp
public static const StageSetting None;
```

No debug overlays are drawn.

**Returns** \
[StageSetting](../../../Murder/Editor/Assets/StageSetting.html) \

#### ShowSound

```csharp
public static const StageSetting ShowSound;
```

Draw an icon/gizmo at the position of entities with sound emitters.

**Returns** \
[StageSetting](../../../Murder/Editor/Assets/StageSetting.html) \

#### ShowSprite

```csharp
public static const StageSetting ShowSprite;
```

Draw sprite bounding boxes for entities with a sprite component.

**Returns** \
[StageSetting](../../../Murder/Editor/Assets/StageSetting.html) \

#### ShowCollider

```csharp
public static const StageSetting ShowCollider;
```

Draw collider shapes for entities with a collider component. This is the default flag set on a newly created [PersistStageInfo](../../../Murder/Editor/Assets/PersistStageInfo.html).

**Returns** \
[StageSetting](../../../Murder/Editor/Assets/StageSetting.html) \

⚡

# SpriteEventData

**Namespace:** Murder.Editor.Assets \
**Assembly:** Murder.dll

```csharp
public class SpriteEventData
```

Holds per-sprite, per-animation event overrides made by hand in the sprite/animation editor.

**Intent:** Layers designer-authored frame events (added events and explicit deletions) on top of whatever frame events Aseprite already exported for an animation, so a developer can add, replace or remove frame-triggered events -- such as footstep sounds or hit frames -- without editing the source `.aseprite`/`.ase` file.

**Use-case:** One instance is kept per sprite GUID inside [SpriteEventDataManagerAsset.Events](../../../Murder/Editor/Assets/SpriteEventDataManagerAsset.html#events). Populated by the sprite/animation editor (`SpriteEditor`) as the developer adds or removes events, and consumed by the Aseprite importer at atlas-build time via `FilterEventsForAnimation` to merge the overrides into the final sprite asset's animation data.

### ⭐ Constructors

```csharp
public SpriteEventData()
```

Creates a new, empty sprite event data container with no custom additions or deletions.

### ⭐ Properties

#### DeletedEvents

```csharp
public readonly Dictionary<string, HashSet<int>> DeletedEvents;
```

Frame indices, keyed by animation name, whose Aseprite-exported event should be treated as removed even though it still exists in the source file. Populated by [RemoveEvent(string, int)](../../../Murder/Editor/Assets/SpriteEventData.html#removeeventstring-int) when the frame being removed was not one of this object's own [Events](../../../Murder/Editor/Assets/SpriteEventData.html#events) entries.

**Returns** \
[Dictionary\<string, HashSet\<int\>\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \

#### Events

```csharp
public readonly Dictionary<string, Dictionary<int, string>> Events;
```

Custom events added or overridden through the editor, keyed by animation name and then by frame index. A value here always wins over whatever event (if any) Aseprite exported for that frame.

**Returns** \
[Dictionary\<string, Dictionary\<int, string\>\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \

### ⭐ Methods

#### AddEvent(string, int, string)

```csharp
public void AddEvent(string animation, int frame, string message)
```

Adds or replaces the custom event message at `frame` for `animation`. If that frame was previously tracked as deleted (via `RemoveEvent`), the deletion is undone since the frame now has an explicit override again.

**Parameters** \
`animation` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) -- name of the animation the event belongs to. \
`frame` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) -- zero-based frame index within the animation. \
`message` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) -- event message/id to fire when this frame plays. \

#### FilterEventsForAnimation(string, Dictionary&lt;int, string&gt;)

```csharp
public void FilterEventsForAnimation(string animation, ref Dictionary<int, string> events)
```

Applies this object's custom additions ([Events](../../../Murder/Editor/Assets/SpriteEventData.html#events)) and deletions ([DeletedEvents](../../../Murder/Editor/Assets/SpriteEventData.html#deletedevents)) for `animation` on top of `events` in-place. Called by the sprite importer after reading the raw events Aseprite exported for an animation, so the final per-frame event map reflects any manual edits made in the editor.

**Parameters** \
`animation` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) -- name of the animation whose events are being merged. \
`events` `Dictionary<int, string>` -- frame-index-to-message dictionary produced from the Aseprite export; mutated in place. \

#### GetEventsForAnimation(string)

```csharp
public Dictionary<int, string> GetEventsForAnimation(string animation)
```

Returns the mutable custom-events dictionary for `animation` from [Events](../../../Murder/Editor/Assets/SpriteEventData.html#events), creating an empty one and registering it if this is the first custom event added for that animation.

**Parameters** \
`animation` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[Dictionary\<int, string\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \

#### RemoveEvent(string, int)

```csharp
public void RemoveEvent(string animation, int frame)
```

Removes the event at `frame` for `animation`. If the frame was one of this object's own custom [Events](../../../Murder/Editor/Assets/SpriteEventData.html#events), it is simply removed from there; otherwise it must have come from the Aseprite export, so it is recorded in [DeletedEvents](../../../Murder/Editor/Assets/SpriteEventData.html#deletedevents) to be suppressed by `FilterEventsForAnimation`.

**Parameters** \
`animation` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) -- name of the animation the event belongs to. \
`frame` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) -- zero-based frame index within the animation. \

⚡

# SpriteEventData

**Namespace:** Murder.Editor.Assets \
**Assembly:** Murder.dll

```csharp
public class SpriteEventData
```

Holds per-animation custom event overrides for a sprite, including added events and deleted events that override the default data.

**Intent:** Allows game-specific custom event data to be layered on top of Aseprite-exported sprite events without modifying the source file.

**Use-case:** Populated by the sprite event editor and queried at import time to merge custom events into the final sprite asset.

### ⭐ Constructors
```csharp
public SpriteEventData()
```
Creates a new empty sprite event data container.

### ⭐ Properties
#### DeletedEvents
```csharp
public readonly Dictionary<TKey, TValue> DeletedEvents;
```
Maps animation names to sets of frame indices whose events have been explicitly removed.

**Returns** \
[Dictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \
#### Events
```csharp
public readonly Dictionary<TKey, TValue> Events;
```
Maps animation names to per-frame custom event messages added via the editor.

**Returns** \
[Dictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \
### ⭐ Methods
#### GetEventsForAnimation(string)
```csharp
public Dictionary<TKey, TValue> GetEventsForAnimation(string animation)
```
Returns or creates the mutable event dictionary for the specified animation name.

**Parameters** \
`animation` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[Dictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \

#### AddEvent(string, int, string)
```csharp
public void AddEvent(string animation, int frame, string message)
```
Adds or replaces the event message at the given frame for the specified animation.

**Parameters** \
`animation` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`frame` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`message` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### FilterEventsForAnimation(string, Dictionary`2&)
```csharp
public void FilterEventsForAnimation(string animation, Dictionary`2& events)
```
Applies this object's custom additions and deletions on top of the provided `events` dictionary in-place.

**Parameters** \
`animation` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`events` [Dictionary\<TKey, TValue\>&](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \

#### RemoveEvent(string, int)
```csharp
public void RemoveEvent(string animation, int frame)
```
Removes the event at the given frame for the specified animation, tracking it in the deleted-events set.

**Parameters** \
`animation` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`frame` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \



⚡
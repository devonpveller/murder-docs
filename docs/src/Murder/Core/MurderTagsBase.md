# MurderTagsBase

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public class MurderTagsBase
```

Base class that defines the built-in integer tag constants for entity categorization. Game-specific projects extend this class to add their own tags.

**Intent:** Registry of named bitfield constants used to categorize and filter entities by role (e.g., player, trigger).

**Use-case:** Reference these constants when assigning a `Tags` component to an entity or when querying entities by tag in systems.

### ⭐ Constructors
```csharp
public MurderTagsBase()
```

This class should never be instanced

### ⭐ Properties
#### NONE
```csharp
public static const int NONE;
```

The empty tag value (0), used when no tags should be applied or matched.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### PLAYER
```csharp
public static const int PLAYER;
```

Tag bit identifying an entity as a player-controlled character.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### TRIGGER
```csharp
public static const int TRIGGER;
```

Tag bit identifying an entity as a trigger volume that fires interactions on contact.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \


⚡
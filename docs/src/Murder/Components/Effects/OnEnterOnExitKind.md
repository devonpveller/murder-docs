# OnEnterOnExitKind

**Namespace:** Murder.Components.Effects \
**Assembly:** Murder.dll

```csharp
[Flags]
public sealed enum OnEnterOnExitKind : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Flags that describe which kind of entity is allowed to trigger a [OnEnterOnExitComponent](../../../Murder/Components/Effects/OnEnterOnExitComponent.html) area, plus a couple of extra behavior toggles for the trigger.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

**Intent:** Combines "who is allowed to trigger this area" with "extra trigger behavior" in a single flags value assigned to [OnEnterOnExitComponent.Kind](../../../Murder/Components/Effects/OnEnterOnExitComponent.html). `Npc` is defined as `Actors | 0x100`, so it implicitly includes `Actors`; `SkipIfActorInside` and `IgnoreOnDeactivate` are modifiers meant to be OR'd together with an entity-kind flag rather than used on their own.

**Use-case:** Set on `OnEnterOnExitComponent.Kind` to control which entities can fire the area's enter/exit interactions — e.g. `Player` for a player-only trigger, or `Npc | SkipIfActorInside` for an NPC-triggerable area that shouldn't re-fire its enter interaction if an actor is already standing inside when the area is created.

### ⭐ Properties

#### Player

```csharp
public static const OnEnterOnExitKind Player;
```

Only the player entity can trigger this area.

**Returns** \
[OnEnterOnExitKind](../../../Murder/Components/Effects/OnEnterOnExitKind.html) \

#### Actors

```csharp
public static const OnEnterOnExitKind Actors;
```

Actor entities (matched via the "actor" collision layer) can trigger this area.

**Returns** \
[OnEnterOnExitKind](../../../Murder/Components/Effects/OnEnterOnExitKind.html) \

#### Npc

```csharp
public static const OnEnterOnExitKind Npc;
```

NPC entities can trigger this area. Defined as `Actors | 0x100`, so it implicitly also matches `Actors`.

**Returns** \
[OnEnterOnExitKind](../../../Murder/Components/Effects/OnEnterOnExitKind.html) \

#### SkipIfActorInside

```csharp
public static const OnEnterOnExitKind SkipIfActorInside;
```

Modifier flag: do not fire the enter interaction if a qualifying actor is already inside the area (e.g. present when the area entity is created).

**Returns** \
[OnEnterOnExitKind](../../../Murder/Components/Effects/OnEnterOnExitKind.html) \

#### IgnoreOnDeactivate

```csharp
public static const OnEnterOnExitKind IgnoreOnDeactivate;
```

Modifier flag: do not fire the exit interaction when the area entity itself is deactivated.

**Returns** \
[OnEnterOnExitKind](../../../Murder/Components/Effects/OnEnterOnExitKind.html) \

⚡

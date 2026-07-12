# TargetEntity

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public sealed enum TargetEntity : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Declares which entity an interaction component should act on, relative to the entity the interaction is attached to.

**Intent:** Interaction components (e.g. `SendMessageInteraction`, `AddComponentOnInteraction`, `PropagateInteraction`) expose a `Target` field of this type so a designer can choose the target entity declaratively in the editor instead of the interaction being hard-coded to always affect the entity it fired on.

**Use-case:** Set on an interaction component's `Target` field to control which entity receives the effect when the interaction fires. Not every interaction implements every case — check the specific interaction's switch statement for which values it actually handles (for example `DestroyOnInteraction` only implements `Self`).

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### Self

```csharp
public static const TargetEntity Self;
```

The entity the interaction/component is attached to (the one that was interacted with). This is the default `Target` value for most interactions.

**Returns** \
[TargetEntity](../../Murder/Utilities/TargetEntity.html) \

#### Parent

```csharp
public static const TargetEntity Parent;
```

The parent of the interacted entity, resolved via the entity hierarchy (`Entity.TryFetchParent`).

**Returns** \
[TargetEntity](../../Murder/Utilities/TargetEntity.html) \

#### Interactor

```csharp
public static const TargetEntity Interactor;
```

The entity that initiated the interaction (e.g. the player walking into a trigger).

**Returns** \
[TargetEntity](../../Murder/Utilities/TargetEntity.html) \

#### Target

```csharp
public static const TargetEntity Target;
```

An explicitly designated target entity, resolved via an id-target component (e.g. `IdTargetComponent` or `IdTargetCollectionComponent`) on the interacted entity.

**Returns** \
[TargetEntity](../../Murder/Utilities/TargetEntity.html) \

#### CreateNewEntity

```csharp
public static const TargetEntity CreateNewEntity;
```

A brand-new entity is spawned and used as the target, instead of acting on an existing one.

**Returns** \
[TargetEntity](../../Murder/Utilities/TargetEntity.html) \

#### Child

```csharp
public static const TargetEntity Child;
```

Every direct child entity of the interacted entity, resolved via `Entity.Children`.

**Returns** \
[TargetEntity](../../Murder/Utilities/TargetEntity.html) \

#### Player

```csharp
public static const TargetEntity Player;
```

Reserved for targeting the player entity specifically.

**Returns** \
[TargetEntity](../../Murder/Utilities/TargetEntity.html) \

⚡

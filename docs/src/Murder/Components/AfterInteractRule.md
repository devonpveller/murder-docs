# AfterInteractRule

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed enum AfterInteractRule : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Defines what happens to an [InteractOnRuleMatchComponent](../../Murder/Components/InteractOnRuleMatchComponent.html) after the rule it describes has been triggered.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

**Intent:** Controls the lifecycle of a rule-based interaction — whether it can fire again, is disabled, or destroys its entity — via the component's `AfterInteraction` field.

**Use-case:** Set `InteractOnRuleMatchComponent.AfterInteraction` to tune what happens once the entity's `Requirements` criteria are satisfied and the interaction fires: leave the rule armed forever (`Always`), consume it once (`InteractOnlyOnce`), strip the rule component but keep the entity (`RemoveComponent`), or remove the entity entirely (`Destroy`).

### ⭐ Properties

#### InteractOnlyOnce

```csharp
public static const AfterInteractRule InteractOnlyOnce = 0;
```

The default behavior. The rule is expected to only interact once; nothing in the enum value itself removes the component, so a listening system is responsible for treating this value as "fire and forget."

**Returns** \
[AfterInteractRule](../../Murder/Components/AfterInteractRule.html) \

#### Always

```csharp
public static const AfterInteractRule Always = 3;
```

Always interact whenever the rule gets triggered (added or modified), with no cleanup — the same entity can trigger this interaction repeatedly for as long as its requirements keep matching.

**Returns** \
[AfterInteractRule](../../Murder/Components/AfterInteractRule.html) \

#### RemoveComponent

```csharp
public static const AfterInteractRule RemoveComponent = 4;
```

Remove the [InteractOnRuleMatchComponent](../../Murder/Components/InteractOnRuleMatchComponent.html) from the entity after this is triggered, so the rule cannot fire again but the entity itself survives. This is the default `AfterInteraction` value on a freshly-constructed `InteractOnRuleMatchComponent`.

**Returns** \
[AfterInteractRule](../../Murder/Components/AfterInteractRule.html) \

#### Destroy

```csharp
public static const AfterInteractRule Destroy = 5;
```

Destroy the entity once the interaction rule is triggered — useful for one-shot triggers (e.g. a cutscene trigger volume or a pickup) that should disappear entirely after firing.

**Returns** \
[AfterInteractRule](../../Murder/Components/AfterInteractRule.html) \

⚡

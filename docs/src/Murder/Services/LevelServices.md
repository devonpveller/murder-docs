# LevelServices

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public static class LevelServices
```

Helpers for transitioning between game levels (worlds).

**Intent:** Provides a small, intention-revealing API for triggering world/scene switches — immediate or delayed — instead of calling `Game.Instance.QueueWorldTransition` and juggling the active save's `OnBeforeMapSwitch` hook directly at every call site.

**Use-case:** Call `SwitchScene` to immediately transition to a new world asset (e.g. from a level-exit trigger or debug menu). Call `SwitchSceneAfterSeconds` when the transition should be delayed — for example to let a fade-out effect or animation play first — which also stops ambience/SFX audio layers right before the switch so audio doesn't bleed between scenes.

### ⭐ Methods

#### SwitchScene(Guid)

```csharp
public static ValueTask SwitchScene(Guid nextWorldGuid)
```

Immediately queues a transition to the world asset identified by `nextWorldGuid` via `Game.Instance.QueueWorldTransition`, and notifies the active `SaveData` (if any) through `OnBeforeMapSwitch` so save-tracked state can react to the upcoming map change (e.g. recording the player's last known location).

**Parameters** \
`nextWorldGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[ValueTask](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.ValueTask?view=net-7.0) \

#### SwitchSceneAfterSeconds(World, Guid, float)

```csharp
public static ValueTask SwitchSceneAfterSeconds(World world, Guid nextWorldGuid, float seconds)
```

Schedules a transition to `nextWorldGuid` after `seconds` of game time. If `seconds` is `0`, switches immediately via `SwitchScene` without starting a coroutine; otherwise runs `SwitchSceneOnSecondsCoroutine` on `world`. Use this instead of manually delaying a `SwitchScene` call whenever the transition should wait for a fade or cutscene beat to finish first.

**Parameters** \
`world` [World](../../Bang/World.html) \
`nextWorldGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`seconds` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[ValueTask](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.ValueTask?view=net-7.0) \

#### SwitchSceneOnSecondsCoroutine(Guid, float)

```csharp
public static IEnumerator<Wait> SwitchSceneOnSecondsCoroutine(Guid nextWorldGuid, float seconds)
```

The coroutine backing `SwitchSceneAfterSeconds`: waits `seconds`, stops the `Ambience` and `Sfx` sound layers with a fade-out, then switches to `nextWorldGuid`. Exposed as a public method so callers who already have their own coroutine pipeline can compose it directly instead of going through `SwitchSceneAfterSeconds`.

**Parameters** \
`nextWorldGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`seconds` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[IEnumerator\<Wait\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerator-1?view=net-7.0) \

⚡

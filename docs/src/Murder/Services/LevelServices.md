# LevelServices

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public static class LevelServices
```

Helpers for transitioning between game levels (worlds).

**Intent:** Provides a clean API for triggering world/scene switches, with optional delays and coroutine helpers.

**Use-case:** Call `SwitchScene` to immediately transition to a new world asset, or `SwitchSceneAfterSeconds` to delay the transition while a fade-out effect plays.

### ⭐ Methods
#### SwitchSceneOnSecondsCoroutine(Guid, float)
```csharp
public IEnumerator<T> SwitchSceneOnSecondsCoroutine(Guid nextWorldGuid, float seconds)
```
A coroutine that waits for `seconds`, stops ambient and SFX layers, then switches to the target world.

**Parameters** \
`nextWorldGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`seconds` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[IEnumerator\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerator-1?view=net-7.0) \

#### SwitchScene(Guid)
```csharp
public ValueTask SwitchScene(Guid nextWorldGuid)
```
Immediately queues a transition to the world identified by `nextWorldGuid` and records it in the active save.

**Parameters** \
`nextWorldGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[ValueTask](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.ValueTask?view=net-7.0) \

#### SwitchSceneAfterSeconds(World, Guid, float)
```csharp
public ValueTask SwitchSceneAfterSeconds(World world, Guid nextWorldGuid, float seconds)
```
Schedules a world transition after a delay; if `seconds` is 0 the switch happens immediately.

**Parameters** \
`world` [World](../../Bang/World.html) \
`nextWorldGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`seconds` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[ValueTask](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.ValueTask?view=net-7.0) \



⚡
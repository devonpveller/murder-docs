# CameraServices

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public static class CameraServices
```

Provides utility methods for controlling the game camera.

**Intent:** Exposes high-level camera operations such as screen-shake to game systems and interactions.

**Use-case:** Call `ShakeCamera` to add physical impact feedback or dramatic screen movement; use the secondary-target helpers to make the camera follow an entity other than the player temporarily.

### ⭐ Methods
#### ShakeCamera(World, float, float)
```csharp
public void ShakeCamera(World world, float intensity, float time)
```
Applies a screen-shake effect with the given intensity for the specified duration; uses the stronger value if a shake is already active.

**Parameters** \
`world` [World](../../Bang/World.html) \
`intensity` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`time` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \



⚡
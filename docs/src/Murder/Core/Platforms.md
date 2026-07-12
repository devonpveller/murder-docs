# Platforms

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public sealed enum Platforms : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Identifies the platform (or family of platforms) a game is running on or is being built for.

**Intent:** Used to gate platform-specific behavior (e.g. input prompts, save paths, storefront integrations) without scattering `#if` compile-time checks through gameplay code — a single runtime value can be checked and branched on instead.

**Use-case:** Compare against the game's current target platform when deciding which control-prompt icons to show, which save/telemetry backend to use, or whether to enable a storefront-specific feature.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### All

```csharp
public static const Platforms All;
```

Wildcard value meaning "any platform" / no specific platform restriction.

**Returns** \
[Platforms](../../Murder/Core/Platforms.html) \

#### Linux

```csharp
public static const Platforms Linux;
```

Desktop Linux.

**Returns** \
[Platforms](../../Murder/Core/Platforms.html) \

#### MacOS

```csharp
public static const Platforms MacOS;
```

Desktop macOS.

**Returns** \
[Platforms](../../Murder/Core/Platforms.html) \

#### PSX

```csharp
public static const Platforms PSX;
```

PlayStation consoles.

**Returns** \
[Platforms](../../Murder/Core/Platforms.html) \

#### SteamDeck

```csharp
public static const Platforms SteamDeck;
```

Valve's Steam Deck handheld.

**Returns** \
[Platforms](../../Murder/Core/Platforms.html) \

#### Switch

```csharp
public static const Platforms Switch;
```

Nintendo Switch.

**Returns** \
[Platforms](../../Murder/Core/Platforms.html) \

#### Windows

```csharp
public static const Platforms Windows;
```

Desktop Windows.

**Returns** \
[Platforms](../../Murder/Core/Platforms.html) \

#### Xbox

```csharp
public static const Platforms Xbox;
```

Xbox consoles.

**Returns** \
[Platforms](../../Murder/Core/Platforms.html) \

⚡

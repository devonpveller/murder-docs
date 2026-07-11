# FileHelper

**Namespace:** Murder.Serialization \
**Assembly:** Murder.dll

```csharp
public static class FileHelper
```

Collection of static helper methods for file path manipulation, platform-specific extensions, and save-file path resolution.

**Intent:** Provides OS-agnostic file system utilities used throughout the engine for locating resources, cleaning asset names, and resolving save paths.

**Use-case:** Call `GetPath(paths)` to resolve a resource path relative to the game's executable, `GetSaveBasePath(gameName)` to locate user save data, and `Clean(str)` to sanitize asset name strings.

### ⭐ Methods
#### Clean(string)
```csharp
public ReadOnlySpan<T> Clean(string str)
```
Strips non-alphanumeric characters (except path separators and hyphens) from `str` and normalizes path separators.

**Parameters** \
`str` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[ReadOnlySpan\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.ReadOnlySpan-1?view=net-7.0) \

#### EscapePath(string)
```csharp
public string EscapePath(string path)
```
Normalizes all path separators in `path` to the current operating system's directory separator character.

**Parameters** \
`path` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### ExtensionForOperatingSystem()
```csharp
public string ExtensionForOperatingSystem()
```

Returns the assembly extension for the target operating system.
            For example, if targeting Windows, this returns ".dll".

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
\

**Exceptions** \
[PlatformNotSupportedException](https://learn.microsoft.com/en-us/dotnet/api/System.PlatformNotSupportedException?view=net-7.0) \
\
#### GetPath(String[])
```csharp
public string GetPath(String[] paths)
```

Gets the rooted path from a relative one

**Parameters** \
`paths` [string[]](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
\

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
\

#### GetPathWithoutExtension(string)
```csharp
public string GetPathWithoutExtension(string path)
```
Returns `path` with the file extension removed, preserving the directory structure.

**Parameters** \
`path` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### GetSaveBasePath(string)
```csharp
public string GetSaveBasePath(string gameName)
```

Gets the base path for save files.

**Parameters** \
`gameName` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \



⚡
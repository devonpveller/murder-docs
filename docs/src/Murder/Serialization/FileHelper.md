# FileHelper

**Namespace:** Murder.Serialization \
**Assembly:** Murder.dll

```csharp
public static partial class FileHelper
```

Static, stateless helpers for file-path manipulation and a handful of OS-specific file-system operations (locating the save directory, opening a folder in the OS file explorer, resolving the native library extension).

**Intent:** Centralize the OS-agnostic path arithmetic and platform-detection logic the engine needs, so the rest of Murder doesn't sprinkle `OperatingSystem.Is*()` checks or raw `Path`/separator handling everywhere. Everything here is pure string/path logic or thin OS interop — actual file reading/writing goes through [FileManager](../../Murder/Serialization/FileManager.html) instead.

**Use-case:** Call `GetPath(paths)` to resolve any Murder-relative resource path (assets, save data, packed content) to an absolute path rooted at the game's content directory, `GetSaveBasePath(gameName)` to locate the per-OS save-data root, and `Clean(str)`/`EscapePath()` to sanitize/normalize asset name strings before using them as path fragments.

### ⭐ Methods

#### Clean(string)

```csharp
public static ReadOnlySpan<char> Clean(string str)
```

Strips any character that isn't a letter, digit, space, hyphen, or path separator from `str`, then normalizes the remaining separators via `EscapePath()`. Used to turn a user/editor-authored asset or folder name into a safe relative path fragment, e.g. when building an editor asset's on-disk path from its display name.

**Parameters** \
`str` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[ReadOnlySpan\<char\>](https://learn.microsoft.com/en-us/dotnet/api/System.ReadOnlySpan-1?view=net-7.0) \

#### EscapePath(string)

```csharp
public static string EscapePath(this string path)
```

Extension method that replaces every `\` and `/` in `path` with the current OS's `Path.DirectorySeparatorChar`. Use this when a path was authored or stored with a hard-coded separator (for example, one embedded in a JSON asset saved on a different OS) and needs to resolve correctly on the machine the game is currently running on.

**Parameters** \
`path` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### ExtensionForOperatingSystem()

```csharp
public static string ExtensionForOperatingSystem()
```

Returns the native shared-library extension for the current operating system (`.dll` on Windows, `.so` on Linux, `.dylib` on macOS). Used when locating/loading platform-specific native libraries at runtime.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Exceptions** \
[PlatformNotSupportedException](https://learn.microsoft.com/en-us/dotnet/api/System.PlatformNotSupportedException?view=net-7.0) — thrown on an operating system other than Windows, Linux, or macOS (e.g. consoles), which are not yet supported. \

#### GetPath(String[])

```csharp
public static string GetPath(params string[] paths)
```

Joins `paths` and resolves the result to an absolute, rooted path. If the joined path is already rooted (e.g. an absolute path chosen by the user in the editor) it is returned unchanged; otherwise it is treated as relative to `Microsoft.Xna.Framework.TitleLocation.Path` (the game's content root, resolved per-platform by FNA) and made absolute. This is the standard way to turn any Murder-relative resource path into a path usable with `File`/`Directory` APIs — it is called throughout `GameDataManager` and the editor's importers/asset managers whenever a relative asset or resource path needs to become a real file-system path.

**Parameters** \
`paths` [string[]](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) — path segments to join before resolving. \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) — the absolute, rooted path. \

#### GetPathWithoutExtension(string)

```csharp
public static string GetPathWithoutExtension(string path)
```

Returns `path` with the file extension removed, preserving the directory structure (e.g. `images/foo.png` becomes `images/foo`). Commonly used to turn a packed texture or resource file path back into the logical asset name used to look it up at runtime.

**Parameters** \
`path` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### GetSaveBasePath(string)

```csharp
public static string GetSaveBasePath(string gameName)
```

Resolves the OS-appropriate root directory for persisted save data belonging to `gameName` — `%LOCALAPPDATA%\{gameName}` on Windows, `~/Library/Application Support/{gameName}` on macOS, the `XDG_DATA_HOME`/`$HOME/.local/share` directory on Linux/BSD, or SDL's platform pref path as a fallback. Called by `GameDataManager` to locate the save directory; useful directly if you need to know where save files live for diagnostics or platform-specific tooling.

**Parameters** \
`gameName` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### GetScreenshotFolder()

```csharp
public static string GetScreenshotFolder()
```

Returns the OS's "My Pictures" special folder, used as the default destination for in-game screenshots.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### OpenFolderOnOS(string)

```csharp
public static void OpenFolderOnOS(string filePath)
```

Opens the native OS file explorer with `filePath` selected/highlighted (Windows Explorer, macOS Finder, or the Linux file manager registered for `xdg-open`). Used by editor tooling (e.g. "open containing folder" actions after saving a screenshot or exporting a file) to jump straight to the file on disk; on an unrecognized OS it just prints the path to the console instead.

**Parameters** \
`filePath` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

⚡

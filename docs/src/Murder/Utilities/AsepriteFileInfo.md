# AsepriteFileInfo

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public sealed struct AsepriteFileInfo
```

Stores metadata for a single frame region within an Aseprite sprite sheet, including the source file path, layer index, slice index, and bake status.

**Intent:** Identifies a specific slice within an Aseprite source file so the asset pipeline can locate and pack the correct frame data.

**Use-case:** Populated automatically during asset import; read by the sprite pipeline to build atlases and resolve animation frames.

### ⭐ Constructors
```csharp
public AsepriteFileInfo()
```

### ⭐ Properties
#### Baked
```csharp
public bool Baked;
```

Whether this entry has been processed and written into the packed sprite atlas.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Layer
```csharp
public int Layer;
```

The Aseprite layer index this entry belongs to.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### SliceIndex
```csharp
public int SliceIndex;
```

The slice index within the Aseprite file that this entry represents.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Source
```csharp
public string Source;
```

The relative path to the source Aseprite (`.ase` or `.aseprite`) file.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \


⚡
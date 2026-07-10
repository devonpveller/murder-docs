# Hello World

We created a sample hello world app on [Hello Murder](https://github.com/isadorasophia/hellomurder). We should cover more on that soon. 

You can take a peek at [IMurderGame](../Murder/IMurderGame.html) on tweaking basic functionality into your game, but a lot of things should be ready to go from the editor project.

---

## Setting Up a New Game with Murder from Scratch

### 1. Create a new game project

```bash
mkdir MyGame && cd MyGame
dotnet new sln --name MyGame       # create a new solution
dotnet new console --name MyGame   # create a console (game) project
dotnet sln add MyGame/MyGame.csproj
```

Edit `MyGame/MyGame.csproj`:

```xml
<PropertyGroup>
  <TargetFramework>net8.0</TargetFramework>
  <OutputType>WinExe</OutputType>
</PropertyGroup>
```

> **Note:** You do **not** need to add FNA manually. Murder depends on the `Murder.FNA` NuGet package, which is pulled in automatically when you reference Murder.

### 2. Add Murder as a submodule

```bash
git submodule add https://github.com/isadorasophia/murder.git libs/murder
git submodule update --init --recursive
```

The `--recursive` flag is important — Murder itself depends on the [Bang](https://github.com/isadorasophia/bang) ECS framework and the [Gum](https://github.com/isadorasophia/gum) UI library, both of which are submodules that must be initialized for Murder to build.

### 3. Reference Murder in your game's `.csproj`

In your game's `.csproj`, add:

```xml
<ItemGroup>
  <ProjectReference Include="..\libs\murder\src\Murder\Murder.csproj" />
</ItemGroup>
```

### 4. Create an editor project for your game

```bash
dotnet new console --name MyGame.Editor
dotnet sln add MyGame.Editor/MyGame.Editor.csproj
```

Then update `MyGame.Editor.csproj`:

```xml
<ItemGroup>
  <ProjectReference Include="..\libs\murder\src\Murder\Murder.csproj" />
  <ProjectReference Include="..\libs\murder\src\Murder.Editor\Murder.Editor.csproj" />
</ItemGroup>
```

Build and run:

```bash
cd MyGame.Editor
dotnet build
dotnet run
```

### 5. Implement your game

Create a class that implements [`IMurderGame`](../Murder/IMurderGame.html). At minimum you'll override `Name` and call `base` lifecycle methods:

```csharp
public class MyGame : IMurderGame
{
    public string Name => "My Game";

    public void Initialize() { /* one-time startup */ }
    public Task LoadContentAsync() => Task.CompletedTask;
    // ... other lifecycle hooks as needed
}
```

See the [IMurderGame](../Murder/IMurderGame.html) docs for the full list of lifecycle callbacks and factory methods.

# Tools & Setup - Development Environment

**Navigation**: [BlockCore](../../README.md) > [Learning](../README.md) > [Prerequisites](overview.md) > [Tools & Setup](tools-setup.md)

Setting up your development environment for BlockCore engine development.

## 🛠️ Required Tools

### 1. .NET 9 SDK
**Purpose**: C# runtime and development tools

**Download**: https://dotnet.microsoft.com/download/dotnet/9.0

**Verify Installation**:
```bash
dotnet --version
# Should show: 9.0.x
```

### 2. IDE (Choose One)

#### Visual Studio 2022 (Recommended)
**Download**: https://visualstudio.microsoft.com/vs/
**Required Workloads**:
- .NET desktop development
- Game development with C++ (for graphics debugging)

**Pros**: Best C# support, integrated debugging, IntelliSense
**Cons**: Windows only, large download

#### JetBrains Rider
**Download**: https://www.jetbrains.com/rider/
**Required Plugins**: None (C# support built-in)

**Pros**: Cross-platform, excellent C# support, lightweight
**Cons**: Paid (free trial available)

#### Visual Studio Code
**Download**: https://code.visualstudio.com/
**Required Extensions**:
- C# Dev Kit
- C# Extensions
- GitLens

**Pros**: Free, lightweight, cross-platform
**Cons**: Less integrated than full IDEs

### 3. Git
**Purpose**: Version control

**Download**: https://git-scm.com/

**Verify Installation**:
```bash
git --version
# Should show: git version 2.x.x
```

## 🎮 Graphics Development Tools

### 1. Graphics Drivers
**Purpose**: Access to latest graphics APIs

**NVIDIA**: https://www.nvidia.com/drivers/
**AMD**: https://www.amd.com/support/
**Intel**: https://www.intel.com/content/www/us/en/support/articles/000005629/graphics.html

### 2. Graphics Debugging Tools

#### RenderDoc (Cross-platform)
**Purpose**: Graphics debugging and profiling
**Download**: https://renderdoc.org/

**Features**:
- Frame capture and analysis
- Shader debugging
- API call inspection

#### NVIDIA Nsight Graphics (NVIDIA GPUs)
**Purpose**: Advanced graphics debugging
**Download**: https://developer.nvidia.com/nsight-graphics

#### AMD Radeon GPU Profiler (AMD GPUs)
**Purpose**: AMD-specific graphics profiling
**Download**: https://gpuopen.com/radeon-gpu-profiler/

## 📊 Performance Profiling Tools

### 1. dotTrace (JetBrains)
**Purpose**: .NET performance profiling
**Download**: https://www.jetbrains.com/profiler/

**Features**:
- Memory allocation tracking
- Method execution time
- Garbage collection analysis

### 2. PerfView (Microsoft)
**Purpose**: Free .NET performance analysis
**Download**: https://github.com/Microsoft/perfview

### 3. BenchmarkDotNet
**Purpose**: Micro-benchmarking
**Installation**:
```bash
dotnet add package BenchmarkDotNet
```

## 🎨 Asset Creation Tools (Optional)

### 1. Blender (3D Modeling)
**Purpose**: Create 3D models and textures
**Download**: https://www.blender.org/

**BlockCore Use Cases**:
- Creating block models
- Texture creation
- Asset optimization

### 2. GIMP (Image Editing)
**Purpose**: Texture editing and creation
**Download**: https://www.gimp.org/

**Alternative**: Adobe Photoshop, Paint.NET

### 3. Audacity (Audio Editing)
**Purpose**: Sound effect creation
**Download**: https://www.audacityteam.org/

## 🔧 Development Environment Setup

### 1. Project Structure
```
BlockCore/
├─ src/
│   ├─ BlockCore.Core/
│   ├─ BlockCore.Render/
│   ├─ BlockCore.Voxel/
│   └─ BlockCore.Examples.Basic/
├─ tests/
├─ docs/
└─ BlockCore.sln
```

### 2. IDE Configuration

#### Visual Studio 2022
1. **Open**: BlockCore.sln
2. **Set Startup Project**: BlockCore.Examples.Basic
3. **Configure Debugging**:
   - Working Directory: `$(ProjectDir)`
   - Command Arguments: (none)

#### Rider
1. **Open**: BlockCore.sln
2. **Set Run Configuration**: BlockCore.Examples.Basic
3. **Configure Debugging**: Same as Visual Studio

#### VS Code
1. **Open**: BlockCore folder
2. **Install Extensions**: C# Dev Kit
3. **Configure Launch**: `.vscode/launch.json`

### 3. Build Configuration

**Debug Build**:
```bash
dotnet build -c Debug
```

**Release Build**:
```bash
dotnet build -c Release
```

**Run Tests**:
```bash
dotnet test
```

## 🌐 Cross-Platform Considerations

### Windows Development
- **Graphics API**: DirectX 12, Vulkan
- **IDE**: Visual Studio 2022 (recommended)
- **Debugging**: Visual Studio debugger

### Linux Development
- **Graphics API**: Vulkan, OpenGL
- **IDE**: Rider or VS Code
- **Debugging**: GDB or Rider debugger

### macOS Development
- **Graphics API**: Metal, Vulkan
- **IDE**: Rider or VS Code
- **Debugging**: LLDB or Rider debugger

## 📚 Additional Tools

### 1. Git GUI (Optional)
**GitHub Desktop**: https://desktop.github.com/
**GitKraken**: https://www.gitkraken.com/
**SourceTree**: https://www.sourcetreeapp.com/

### 2. Package Managers
**NuGet**: Built into .NET SDK
**Chocolatey** (Windows): https://chocolatey.org/
**Homebrew** (macOS/Linux): https://brew.sh/

### 3. Documentation Tools
**DocFX**: Generate API documentation
**Markdown Editors**: Typora, Mark Text

## 🚀 Verification Steps

### 1. Test .NET Installation
```bash
dotnet new console -n TestApp
cd TestApp
dotnet run
# Should print: Hello, World!
```

### 2. Test Graphics API Access
Create a simple test to verify graphics drivers:
```csharp
// This will be covered in v0.1 implementation
```

### 3. Test Git Integration
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

## 🎯 Next Steps

1. **Install Required Tools**: .NET 9 SDK, IDE, Git
2. **Update Graphics Drivers**: Latest version for your GPU
3. **Clone Repository**: Get BlockCore source code
4. **Build Project**: Verify everything works
5. **Start Learning**: [v0.1 Learning Guide](v0.1/what-you-will-learn.md)

## 🆘 Troubleshooting

### Common Issues

**"dotnet command not found"**:
- Add .NET SDK to PATH
- Restart terminal/IDE

**"Graphics API not available"**:
- Update graphics drivers
- Check GPU compatibility

**"Build errors"**:
- Verify .NET 9 SDK installation
- Check project dependencies

**"Performance issues"**:
- Enable hardware acceleration
- Close unnecessary applications

**📖 Need Help?**: Check the [Troubleshooting Guide](../reference/troubleshooting.md) for detailed solutions to common development environment issues.

---

## 📖 Navigation

**Previous**: [Key Concepts](concepts.md)  
**Next**: [v0.1 Learning Guide](../v0.1/what-you-will-learn.md)

**Ready to start coding? Head to [v0.1 Learning Guide](../v0.1/what-you-will-learn.md)!**

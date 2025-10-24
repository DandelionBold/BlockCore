# BlockCore

**Navigation**: [BlockCore](README.md)

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![.NET](https://img.shields.io/badge/.NET-9.0-purple.svg)](https://dotnet.microsoft.com/)
[![Status](https://img.shields.io/badge/Status-In%20Development-yellow.svg)]()

**A modular, open-source voxel game engine powering sandbox worlds.**

BlockCore is a high-performance game engine built with C# and .NET 9, designed specifically for voxel-based games. It provides the foundational systems for rendering, physics, world generation, networking, plugins, and resource management—everything needed to build immersive sandbox experiences like [MineWorld](https://github.com/DandelionBold/MineWorld).

---

## 🎯 Features

- **🎨 High-Performance Rendering**: Modern graphics pipeline with greedy meshing, shader support, and optimized chunk rendering
- **🌍 Infinite Procedural Worlds**: Deterministic world generation from seeds with configurable biomes and structures
- **⚡ Physics Engine**: AABB collision detection, character controller, and voxel-based physics
- **🔌 Plugin System**: Sandboxed Lua/JS plugin host with versioned APIs and capability checks
- **📦 Resource Packs**: VFS-based pack system supporting textures, models, shaders, and localization
- **🌐 Networking**: Client-server architecture with chunk streaming and authoritative server
- **💾 Save System**: Compressed region files with atomic writes and version migration
- **⚙️ Configuration**: TOML/JSON-based config with hot-reload support

---

## 🏗️ Architecture

```
BlockCore/
  ├─ Core/         # App loop, platform abstraction, job system
  ├─ Render/       # GPU abstraction, materials, shaders
  ├─ Voxel/        # Blocks, chunks, meshing, lighting
  ├─ WorldGen/     # Noise generation, biome system
  ├─ Physics/      # Collision detection, character controller
  ├─ Commands/     # Command dispatcher, permissions
  ├─ Resources/    # VFS, pack loader, hot-reload
  ├─ Plugins/      # Plugin host, sandbox, event bus
  ├─ IO/           # Save format, compression, backups
  ├─ Net/          # Protocol, serialization, replication
  └─ Config/       # Configuration system
```

---

## 🚀 Getting Started

> **Note**: BlockCore is currently in early development (v0.1). APIs are subject to change.

### Prerequisites

- [.NET 9 SDK](https://dotnet.microsoft.com/download/dotnet/9.0)
- Windows 10/11, Linux, or macOS
- GPU with Vulkan/DirectX 12/Metal support

### Building from Source

```bash
# Clone the repository
git clone https://github.com/DandelionBold/BlockCore.git
cd BlockCore

# Build the engine
dotnet build

# Run tests
dotnet test
```

### Using BlockCore in Your Game

```bash
# Add BlockCore as a dependency
dotnet add package BlockCore --version 0.1.0-preview
```

---

## 📚 Documentation

- **🎓 Learning Path**: [Comprehensive guides](docs/learning/README.md) for developers transitioning from enterprise development to game engine development
- [Planning & Roadmap](docs/planning/overall.md) - Long-term vision and architecture
- [v0.1 Development Plan](docs/planning/v0.1.md) - Current milestone details
- [API Documentation](docs/api/README.md) - Complete API reference
- [Tutorials](docs/tutorials/README.md) - Step-by-step guides

---

## 🎮 Example Games

- [**MineWorld**](https://github.com/DandelionBold/MineWorld) - A voxel sandbox game built on BlockCore

---

## 🛠️ Development

BlockCore follows semantic versioning (MAJOR.MINOR.PATCH):
- **MAJOR**: Breaking API changes
- **MINOR**: New features (backward compatible)
- **PATCH**: Bug fixes only

### Current Roadmap

- **v0.1** - Foundation (window, rendering, single chunk, camera)
- **v0.2** - World generation & saves
- **v0.3** - Physics & editing
- **v0.4** - Commands & resource packs
- **v0.5** - Plugin system
- **v0.6** - Networking
- **v1.0** - Stable API release

---

## 🤝 Contributing

Contributions are welcome! Please read our [contributing guidelines](CONTRIBUTING.md) before submitting PRs.

### Development Guidelines

- **C# Conventions**: 
  - Constants: `SCREAMING_SNAKE_CASE`
  - Variables/Functions: `camelCase`
  - Classes: `PascalCase`
- **Commits**: Reference task plan files in commit messages
- **Branching**: `MAJOR.MINOR.PATCH/feature/<short-slug>`

---

## 📄 License

BlockCore is dual-licensed:
- Code: [Apache License 2.0](LICENSE)
- Example Assets: [CC BY 4.0](LICENSE-CC-BY-4.0)

---

## 🌟 Related Projects

### Core Ecosystem
- **[MineWorld](https://github.com/DandelionBold/MineWorld)** - Reference game implementation built on BlockCore
  - Demonstrates engine capabilities
  - Provides game development examples
  - [Learning Guide](https://github.com/DandelionBold/MineWorld/blob/main/docs/learning/README.md)

### Developer Tools
- **[BlockCore-SDK](https://github.com/DandelionBold/BlockCore-SDK)** - Developer toolkit for engine extensions
  - CLI tools for plugin development
  - Schemas and validation tools
  - [SDK Documentation](https://github.com/DandelionBold/BlockCore-SDK/blob/main/docs/learning/README.md)

- **[MineWorld-SDK](https://github.com/DandelionBold/MineWorld-SDK)** - Modding toolkit for MineWorld
  - Game-specific modding tools
  - Content creation utilities
  - [Modding Guide](https://github.com/DandelionBold/MineWorld-SDK/blob/main/docs/learning/README.md)

---

## 💬 Community

- GitHub Issues: Bug reports and feature requests
- Discussions: Questions and community chat

---

## 📖 Navigation

**Next**: [Learning Path](docs/learning/README.md) | [Planning Documentation](docs/planning/README.md)

**Built with ❤️ by the BlockCore Team**


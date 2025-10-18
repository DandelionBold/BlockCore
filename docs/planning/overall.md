# BlockCore - Overall Vision & Roadmap

**Document Version**: 1.0  
**Last Updated**: 2025-10-18  
**Status**: Living Document

---

## Executive Summary

**BlockCore** is a modular, open-source voxel game engine built with C# and .NET 9, designed to power infinite sandbox worlds with high performance, extensibility, and deterministic behavior. It provides stable, versioned APIs for rendering, physics, world generation, networking, plugins, and resource management—enabling games like MineWorld and future voxel-based experiences to be built on a solid, reusable foundation.

---

## 1. Vision & Philosophy

### 1.1 North Star

**"Provide a reusable, high-performance engine that makes building voxel games a joy, not a journey into low-level complexity."**

### 1.2 Guiding Principles

1. **Reusability First** - Clean, game-agnostic APIs; zero game-specific logic in engine
2. **Data-Oriented & Async** - Cache-friendly hot paths; heavy work off main thread
3. **Deterministic by Design** - Same seed → identical world; testable, reproducible
4. **Extensible & Safe** - Plugin sandboxing, capability-gated features, versioned APIs
5. **Testable & Observable** - Golden tests, metrics, profiling built-in
6. **Modern C# Practices** - .NET 9+, nullable reference types, spans, SIMD where beneficial

---

## 2. Strategic Goals (2025-2030)

### 2.1 Year 1 Goals (2025)

- ✅ **v0.1-v0.3**: Foundation - Rendering, world generation, physics
- ✅ **v0.4-v0.6**: Systems - Commands, plugins, networking
- 🎯 **v1.0**: First stable release with frozen public APIs

### 2.2 Year 2-3 Goals (2026-2027)

- 🎯 **v1.x**: Performance optimization (LOD, occlusion culling, GPU-driven rendering)
- 🎯 **v2.0**: Advanced features (ECS architecture, liquid physics, advanced lighting)
- 🎯 Community growth (3+ games built on BlockCore, 50+ plugins)

### 2.3 Year 4-5 Goals (2028-2030)

- 🎯 **v3.0**: Distributed server architecture (MMO-scale)
- 🎯 **v4.0**: Advanced rendering (ray tracing, GI, volumetric effects)
- 🎯 Industry adoption (used in commercial games, educational institutions)

---

## 3. Architecture Evolution

### 3.1 v0.1-v1.0 Architecture (Foundation Phase)

```
┌──────────────────────────────────────────────────────┐
│                   Game Layer                         │
│            (MineWorld, Future Games)                 │
└───────────────────┬──────────────────────────────────┘
                    │ Public Stable APIs
┌───────────────────┴──────────────────────────────────┐
│               BlockCore Engine (v1.0)                │
│  ┌──────────┬─────────┬──────────┬─────────────┐    │
│  │ Render   │ Voxel   │ Physics  │ WorldGen    │    │
│  ├──────────┼─────────┼──────────┼─────────────┤    │
│  │ Commands │ Plugins │ Resources│ Net         │    │
│  ├──────────┼─────────┼──────────┼─────────────┤    │
│  │ Core     │ IO      │ Config   │ Utilities   │    │
│  └──────────┴─────────┴──────────┴─────────────┘    │
└──────────────────────────────────────────────────────┘
```

**Characteristics**:
- Monolithic libraries with modular internal structure
- Synchronous main loop with async workers
- CPU-driven rendering with GPU batching
- Single-threaded world gen with job workers

### 3.2 v2.0 Architecture (Performance Phase)

**Key Changes**:
- Optional ECS architecture for high entity count
- Multi-threaded chunk generation pipeline
- GPU compute for advanced meshing
- Spatial partitioning improvements

### 3.3 v3.0+ Architecture (Scale Phase)

**Key Changes**:
- Distributed server backend (shard support)
- Cloud save integration
- Advanced networking (delta compression, interest management)
- Ray-traced lighting option

---

## 4. Capability Roadmap

### v0.1 - Foundation (3-6 months)

**Focus**: Prove the tech stack; get pixels on screen

#### Core Systems
- [ ] Window management (cross-platform via Silk.NET)
- [ ] Render loop with frame timing
- [ ] Job system (thread pool for async work)
- [ ] Basic logging & profiling

#### Rendering
- [ ] GPU abstraction layer (Vulkan/DirectX/Metal via Silk.NET)
- [ ] Single flat chunk → vertex mesh → draw
- [ ] Camera system (FPS-style movement)
- [ ] Basic shader pipeline

#### Voxel
- [ ] Block definition structure
- [ ] 16×16×16 chunk sections
- [ ] Simple greedy meshing (opaque blocks only)

**Deliverables**: Window displays one rendered chunk; camera moves around it

---

### v0.2 - World & Saves (2-4 months)

**Focus**: Infinite procedural worlds; persistence

#### WorldGen
- [ ] Seeded RNG utilities
- [ ] 2D/3D noise library (OpenSimplex/Perlin)
- [ ] Heightmap-based terrain generation
- [ ] Biome API hooks (game defines biomes)

#### Voxel Improvements
- [ ] Chunk manager (loading/unloading by distance)
- [ ] Skylight propagation (simple flood-fill)
- [ ] Block light sources

#### IO
- [ ] World metadata format (`world.json`)
- [ ] Region file format (`.bcr` - BlockCore Region)
- [ ] Compression (zstd)
- [ ] Save/load world

**Deliverables**: Create world with seed → infinite terrain → save → reload → identical

---

### v0.3 - Physics & Editing (2-3 months)

**Focus**: Player interaction; collision

#### Physics
- [ ] AABB collision detection (swept tests)
- [ ] Character controller (step height, slope limits)
- [ ] Gravity simulation
- [ ] Ground detection & jump

#### Voxel Editing
- [ ] Place/break block API
- [ ] Dirty chunk remeshing (incremental)
- [ ] Collision shape updates

#### Resources
- [ ] Basic VFS (virtual file system)
- [ ] Texture loading (PNG/DDS)
- [ ] Texture atlas generation

**Deliverables**: Player walks, collides, places/breaks blocks; changes persist

---

### v0.4 - Commands & Packs (2-3 months)

**Focus**: Content extensibility

#### Commands
- [ ] Typed parameter system (`int`, `float`, `enum`, `vec3`, `selector`)
- [ ] Command dispatcher
- [ ] Permission system (`player`, `op`, `server`)
- [ ] Autocomplete metadata

#### Resources (Extended)
- [ ] Resource pack manifest format
- [ ] Pack loading (folder or zip)
- [ ] Hot-reload for textures/models
- [ ] Localization (i18n) infrastructure

#### Config
- [ ] TOML/JSON config loader
- [ ] Schema validation
- [ ] Config overlays (defaults + user overrides)

**Deliverables**: Load multiple texture packs; hot-swap them; run typed commands

---

### v0.5 - Plugins (3-4 months)

**Focus**: Modding support

#### Plugin System
- [ ] Lua host (via NLua or MoonSharp)
- [ ] Plugin manifest format
- [ ] Lifecycle hooks (`onLoad`, `onEnable`, `onDisable`, `onTick`)
- [ ] Event bus (subscribe/publish pattern)
- [ ] Sandbox limits (CPU budget, memory cap)

#### Plugin APIs
- [ ] Commands API (register custom commands)
- [ ] Blocks API (read/write voxels safely)
- [ ] Players API (teleport, inventory access)
- [ ] Storage API (key-value per plugin)

**Deliverables**: Load sample plugins; execute custom commands; plugins hook events

---

### v0.6 - Networking (4-6 months)

**Focus**: Multiplayer

#### Networking
- [ ] Protocol design (versioned, little-endian)
- [ ] Client-server architecture (authoritative server)
- [ ] Reliable/unreliable channels (TCP + UDP via LiteNetLib)
- [ ] Chunk streaming (distance-based prioritization)
- [ ] Snapshot + delta compression

#### Server
- [ ] Headless server mode (no rendering)
- [ ] Player join/leave handling
- [ ] Auth hooks (pluggable authentication)
- [ ] Whitelist/banlist

#### Client
- [ ] Server connection UI
- [ ] Latency prediction (client-side movement prediction)
- [ ] Chunk receive & cache

**Deliverables**: Run dedicated server; connect 2+ clients; synchronized world state

---

### v1.0 - Stable Release (Polishing phase)

**Focus**: API freeze, documentation, production-ready

- [ ] API review & freeze (no breaking changes in v1.x)
- [ ] Comprehensive documentation (API docs + tutorials)
- [ ] Performance benchmarks (target 60 FPS @ 16 chunks render distance)
- [ ] Backward-compatible save migration system
- [ ] Example game (MineWorld v1.0) shipping
- [ ] SDK tools (BlockCore-SDK v1.0) ready

**Success Criteria**:
- ✅ Stable for 6+ months without breaking changes
- ✅ 3+ community games using BlockCore
- ✅ 50+ plugins/packs created with SDK tools

---

### v2.0+ - Advanced Features (Future)

#### Performance
- [ ] Chunk LOD (level-of-detail)
- [ ] GPU occlusion culling
- [ ] GPU-driven rendering (indirect draw)
- [ ] SIMD optimizations for meshing

#### Rendering
- [ ] PBR materials (metallic/roughness)
- [ ] Dynamic shadows (cascaded shadow maps)
- [ ] Post-processing stack (bloom, AO, tonemapping)
- [ ] Shader pack capability system

#### Gameplay
- [ ] Lightweight ECS (optional)
- [ ] Liquid physics (water/lava flow)
- [ ] Advanced lighting (GI approximation)
- [ ] Structure generation framework

#### Scale
- [ ] Distributed server backend (multiple shards)
- [ ] Cloud save integration
- [ ] Large-scale servers (>100 players)

---

## 5. Technology Stack Evolution

### v0.1-v1.0 Stack (Current)

| Component | Technology | Rationale |
|-----------|-----------|-----------|
| **Language** | C# 12 | Productivity, safety, modern features |
| **Runtime** | .NET 9 | Performance, cross-platform, tooling |
| **Graphics** | Silk.NET (Vulkan/DX12/Metal) | Modern, low-level, cross-platform |
| **Windowing** | Silk.NET.Windowing | Integrated with graphics |
| **Networking** | LiteNetLib | Proven, RUDP, open-source |
| **Scripting** | MoonSharp (Lua) | Sandboxable, fast, C#-friendly |
| **Compression** | ZstdSharp | High compression ratio, fast |
| **Config** | Tomlyn (TOML) | Human-readable, typed |
| **Testing** | xUnit + FluentAssertions | Industry standard |

### v2.0+ Potential Evolution

- **ECS**: Consider Arch or custom implementation
- **Physics**: Integrate Jitter2 or BepuPhysics v2
- **Scripting**: Add JS runtime option (Jint or V8)
- **Rendering**: Evaluate GPU-driven pipelines

---

## 6. Integration with Ecosystem

### 6.1 Relationship with MineWorld

```
BlockCore (Engine)
    ↓ provides APIs
MineWorld (Game)
    ↓ produces
Client + Server Executables
```

**Contracts**:
- MineWorld depends on BlockCore via NuGet package
- MineWorld declares compatible engine version range
- Breaking changes in BlockCore require MineWorld update

### 6.2 Relationship with BlockCore-SDK

```
BlockCore (Engine)
    ↓ defines API contracts
BlockCore-SDK (Tools)
    ↓ documents & validates
Engine Extensions (Plugins/Packs)
    ↓ loaded by
BlockCore (Runtime)
```

**Contracts**:
- SDK mirrors engine public APIs in schemas
- SDK validates extension compatibility
- SDK produces artifacts engine can load

### 6.3 Version Synchronization Strategy

| Phase | BlockCore | MineWorld | BlockCore-SDK | MineWorld-SDK |
|-------|-----------|-----------|---------------|---------------|
| v0.1-v0.6 | Rapid iteration | Tracks closely | Lags 1 version | Lags 1 version |
| v1.0 | API freeze | v1.0 release | v1.0 release | v1.0 release |
| v1.x | Bug fixes only | Features | Features | Features |
| v2.0 | Next major | v2.0 adapts | v2.0 adapts | v2.0 adapts |

---

## 7. Risk Management

### 7.1 Technical Risks

| Risk | Impact | Mitigation |
|------|--------|-----------|
| **C# GC pauses** | High | Object pooling, Span<T>, careful allocations |
| **Cross-platform bugs** | Medium | CI matrix (Windows/Linux/Mac), early testing |
| **API churn before v1.0** | Medium | Experimental namespaces, ADRs for changes |
| **Performance cliffs** | High | Continuous profiling, benchmarks in CI |
| **Save corruption** | Critical | Atomic writes, checksum validation, backups |

### 7.2 Project Risks

| Risk | Impact | Mitigation |
|------|--------|-----------|
| **Scope creep** | High | Lock MVP per version; stretch goals tracked separately |
| **Contributor burnout** | Medium | Modular architecture allows focused contributions |
| **Community fragmentation** | Low | Clear SDK standards, versioned APIs |
| **Legal/licensing** | Low | Apache 2.0 for code, CC-BY-4.0 for assets |

---

## 8. Success Metrics

### v1.0 Metrics (Quantitative)

- ✅ **Performance**: 60 FPS @ 16 chunks render distance on mid-tier GPU
- ✅ **Stability**: 0 crashes in 6-hour soak test
- ✅ **Determinism**: 100% chunk hash match for same seed across platforms
- ✅ **API Coverage**: >80% of public APIs documented with examples
- ✅ **Test Coverage**: >70% code coverage for core systems

### Community Metrics (Qualitative)

- ✅ **Adoption**: 3+ games actively using BlockCore
- ✅ **Ecosystem**: 50+ plugins/packs created with SDK tools
- ✅ **Contributors**: 10+ external contributors
- ✅ **Documentation**: "Getting Started" tutorial completable in <1 hour

---

## 9. Open Questions & Future Decisions

### To Be Decided

- [ ] **ECS**: Build custom or integrate existing? (Decision by v1.5)
- [ ] **Scripting**: Lua-only or add JS runtime? (Decision by v1.3)
- [ ] **Physics**: Keep custom or integrate library? (Decision by v2.0)
- [ ] **Rendering**: Stick with Silk.NET or build custom backend? (Decision by v2.0)
- [ ] **Cloud**: Support cloud saves/multiplayer? (Decision by v2.5)

### Research Needed

- [ ] GPU-driven rendering patterns in .NET
- [ ] Distributed server architectures for voxel games
- [ ] Advanced meshing (surface nets, dual contouring)
- [ ] Ray-traced lighting in voxel engines

---

## 10. Conclusion

BlockCore is a **multi-year commitment** to building a best-in-class voxel engine with C# and .NET. The roadmap is ambitious but achievable through:

1. **Incremental delivery** (working software every 2-3 months)
2. **Community building** (SDKs enable ecosystem growth)
3. **Technical excellence** (performance, determinism, testability)
4. **Sustainability** (modular, documented, extensible)

**The journey from v0.1 to v1.0 is the foundation. Everything after is scale and polish.**

---

## Appendix: Related Documents

- [v0.1 Plan](v0.1.md) - Detailed implementation plan for first milestone
- Architecture Decision Records (ADRs) *(Coming Soon)*
- API Reference *(Coming Soon)*

---

**Last Reviewed**: 2025-10-18  
**Next Review**: After v0.1 completion


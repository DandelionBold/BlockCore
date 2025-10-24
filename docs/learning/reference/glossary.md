# Glossary - Game Development Terminology

**Navigation**: [BlockCore](../../README.md) > [Learning](../README.md) > [Reference](glossary.md)

Essential terms for BlockCore development, explained for enterprise developers.

## A

**API (Application Programming Interface)**
- **Definition**: Interface between software components
- **Game Context**: Graphics API (OpenGL, Vulkan) provides access to GPU
- **Enterprise Analogy**: Like database drivers, but for graphics hardware

**Asset**
- **Definition**: Game content (textures, models, sounds, scripts)
- **Game Context**: Resources loaded by the engine
- **Enterprise Analogy**: Like configuration files, but binary and larger

## B

**Buffer**
- **Definition**: Memory region for storing data
- **Game Context**: GPU memory for vertices, textures, etc.
- **Enterprise Analogy**: Like database buffers, but on graphics card

**Bytecode**
- **Definition**: Intermediate representation of code
- **Game Context**: Compiled shader code for GPU execution
- **Enterprise Analogy**: Like Java bytecode, but for graphics processing

## C

**Chunk**
- **Definition**: Subdivision of game world for memory management
- **Game Context**: 16×16×256 block region in voxel world
- **Enterprise Analogy**: Like database pages, but for 3D space

**Culling**
- **Definition**: Process of not rendering invisible objects
- **Game Context**: Skip rendering objects outside camera view
- **Enterprise Analogy**: Like database query optimization, but for rendering

## D

**Delta Time**
- **Definition**: Time elapsed between frames
- **Game Context**: Used for frame-rate independent movement
- **Enterprise Analogy**: Like request processing time, but continuous

**Draw Call**
- **Definition**: Command to render a batch of geometry
- **Game Context**: Each draw call has CPU overhead
- **Enterprise Analogy**: Like database query, but for rendering

## E

**Entity**
- **Definition**: Game object with components
- **Game Context**: Player, enemy, item, etc.
- **Enterprise Analogy**: Like database record, but with behavior

## F

**Frame**
- **Definition**: Single image in animation sequence
- **Game Context**: One complete render cycle (60 FPS = 60 frames/second)
- **Enterprise Analogy**: Like request-response cycle, but continuous

**Frustum**
- **Definition**: 3D pyramid defining camera's field of view
- **Game Context**: Used for culling objects outside view
- **Enterprise Analogy**: Like database view, but for 3D space

## G

**GPU (Graphics Processing Unit)**
- **Definition**: Specialized processor for graphics operations
- **Game Context**: Handles rendering, shaders, parallel processing
- **Enterprise Analogy**: Like specialized database server, but for graphics

## H

**Hot Reloading**
- **Definition**: Updating code/assets without restarting
- **Game Context**: Modify shaders, textures, scripts during development
- **Enterprise Analogy**: Like live code updates, but for game assets

## I

**Index Buffer**
- **Definition**: Array of indices referencing vertices
- **Game Context**: Defines triangles using vertex indices
- **Enterprise Analogy**: Like foreign keys, but for geometry

## J

**Jitter**
- **Definition**: Unwanted variation in frame timing
- **Game Context**: Causes stuttering, affects smoothness
- **Enterprise Analogy**: Like response time variance, but visual

## L

**LOD (Level of Detail)**
- **Definition**: Reducing complexity at distance
- **Game Context**: Lower polygon count for distant objects
- **Enterprise Analogy**: Like data aggregation, but for geometry

## M

**Mesh**
- **Definition**: Collection of vertices forming 3D geometry
- **Game Context**: 3D model data (vertices, faces, textures)
- **Enterprise Analogy**: Like data structure, but for 3D shapes

**Mipmap**
- **Definition**: Pre-calculated texture at different resolutions
- **Game Context**: Improves performance and visual quality
- **Enterprise Analogy**: Like cached query results, but for textures

## N

**Normal**
- **Definition**: Vector perpendicular to surface
- **Game Context**: Used for lighting calculations
- **Enterprise Analogy**: Like metadata, but for surface orientation

## O

**Occlusion**
- **Definition**: Blocking of one object by another
- **Game Context**: Objects behind walls shouldn't be rendered
- **Enterprise Analogy**: Like data filtering, but for visibility

## P

**Pipeline**
- **Definition**: Sequence of processing stages
- **Game Context**: Rendering pipeline (vertex → fragment → screen)
- **Enterprise Analogy**: Like data processing pipeline, but for graphics

**Primitive**
- **Definition**: Basic geometric shape (triangle, line, point)
- **Game Context**: Fundamental building blocks of 3D graphics
- **Enterprise Analogy**: Like data types, but for geometry

## Q

**Quad**
- **Definition**: Four-sided polygon (two triangles)
- **Game Context**: Common primitive for sprites, UI elements
- **Enterprise Analogy**: Like data record, but for 2D shapes

## R

**Rasterization**
- **Definition**: Converting 3D geometry to pixels
- **Game Context**: Process of drawing triangles on screen
- **Enterprise Analogy**: Like data visualization, but for 3D shapes

**Render Target**
- **Definition**: Surface where rendering output is written
- **Game Context**: Screen, texture, or off-screen buffer
- **Enterprise Analogy**: Like output stream, but for graphics

## S

**Shader**
- **Definition**: Program running on GPU
- **Game Context**: Vertex shader (geometry), fragment shader (pixels)
- **Enterprise Analogy**: Like stored procedure, but for graphics

**Stencil Buffer**
- **Definition**: Special buffer for masking operations
- **Game Context**: Used for shadows, reflections, UI clipping
- **Enterprise Analogy**: Like data mask, but for rendering

## T

**Texture**
- **Definition**: Image applied to 3D surface
- **Game Context**: Provides color, detail, material properties
- **Enterprise Analogy**: Like data visualization, but for surfaces

**Transform**
- **Definition**: Mathematical operation on 3D coordinates
- **Game Context**: Move, rotate, scale objects in 3D space
- **Enterprise Analogy**: Like data transformation, but for geometry

## U

**UV Coordinates**
- **Definition**: 2D coordinates mapping texture to 3D surface
- **Game Context**: How texture image is applied to geometry
- **Enterprise Analogy**: Like data mapping, but for textures

## V

**Vertex**
- **Definition**: 3D point in space
- **Game Context**: Corner of triangle, contains position, color, texture coordinates
- **Enterprise Analogy**: Like data point, but in 3D space

**Voxel**
- **Definition**: 3D pixel (volume pixel)
- **Game Context**: 3D block in voxel world (like Minecraft blocks)
- **Enterprise Analogy**: Like database cell, but in 3D space

## W

**World Space**
- **Definition**: Global 3D coordinate system
- **Game Context**: Absolute position of objects in game world
- **Enterprise Analogy**: Like global coordinate system, but for 3D

## X

**X-Axis**
- **Definition**: Horizontal axis in 3D space
- **Game Context**: Left-right direction in world coordinates
- **Enterprise Analogy**: Like X-axis in charts, but in 3D

## Y

**Y-Axis**
- **Definition**: Vertical axis in 3D space
- **Game Context**: Up-down direction in world coordinates
- **Enterprise Analogy**: Like Y-axis in charts, but in 3D

## Z

**Z-Axis**
- **Definition**: Depth axis in 3D space
- **Game Context**: Forward-backward direction in world coordinates
- **Enterprise Analogy**: Like Z-axis in 3D charts

## Common Acronyms

**FPS**: Frames Per Second
**GPU**: Graphics Processing Unit
**CPU**: Central Processing Unit
**API**: Application Programming Interface
**LOD**: Level of Detail
**UV**: Texture coordinates (U, V)
**MVP**: Model-View-Projection (matrix)
**VBO**: Vertex Buffer Object
**VAO**: Vertex Array Object
**FBO**: Framebuffer Object
**SSBO**: Shader Storage Buffer Object

---

## 📖 Navigation

**Previous**: [v0.1 Learning Guide](../v0.1/what-you-will-learn.md)  
**Next**: [Common Patterns](common-patterns.md)

**Need more terms? Check the [Common Patterns](common-patterns.md) for architectural concepts!**

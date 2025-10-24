# Troubleshooting - Common Issues and Solutions

Solutions to common problems encountered during BlockCore development.

## 🚨 Common Issues

### 1. Graphics API Errors

#### "OpenGL context not created"
**Symptoms**: Application crashes on startup
**Causes**: 
- Graphics drivers not installed/updated
- Hardware doesn't support OpenGL
- Multiple OpenGL contexts conflict

**Solutions**:
```csharp
// Check OpenGL support
if (!GL.IsSupported) {
    throw new NotSupportedException("OpenGL not supported");
}

// Create context with proper settings
var context = new GLContext(new ContextSettings {
    API = ContextAPI.OpenGL,
    Version = new Version(3, 3),
    Profile = ContextProfile.Core
});
```

#### "Shader compilation failed"
**Symptoms**: Black screen or rendering errors
**Causes**:
- Syntax errors in shader code
- Incompatible shader versions
- Missing shader inputs/outputs

**Solutions**:
```csharp
// Check shader compilation
if (!shader.Compile()) {
    string error = shader.GetCompileError();
    Console.WriteLine($"Shader error: {error}");
}

// Validate shader program
if (!program.Link()) {
    string error = program.GetLinkError();
    Console.WriteLine($"Program error: {error}");
}
```

### 2. Performance Issues

#### "Low frame rate"
**Symptoms**: Game runs below 60 FPS
**Causes**:
- Too many draw calls
- Inefficient mesh generation
- Memory allocation in render loop
- CPU bottleneck

**Solutions**:
```csharp
// Profile frame time
var stopwatch = Stopwatch.StartNew();
Update(deltaTime);
var updateTime = stopwatch.ElapsedMilliseconds;

stopwatch.Restart();
Render();
var renderTime = stopwatch.ElapsedMilliseconds;

Console.WriteLine($"Update: {updateTime}ms, Render: {renderTime}ms");

// Optimize draw calls
// Batch similar objects together
// Use instanced rendering for repeated objects
```

#### "Memory usage growing"
**Symptoms**: Memory usage increases over time
**Causes**:
- Memory leaks in resource loading
- Objects not being disposed
- Growing collections

**Solutions**:
```csharp
// Use object pooling
public class ObjectPool<T> where T : new() {
    private Queue<T> pool = new Queue<T>();
    
    public T Get() {
        return pool.Count > 0 ? pool.Dequeue() : new T();
    }
    
    public void Return(T obj) {
        pool.Enqueue(obj);
    }
}

// Implement IDisposable
public class Resource : IDisposable {
    private bool disposed = false;
    
    public void Dispose() {
        if (!disposed) {
            // Cleanup resources
            disposed = true;
        }
    }
}
```

### 3. Input Issues

#### "Input not responding"
**Symptoms**: Keyboard/mouse input not working
**Causes**:
- Input events not being polled
- Window not focused
- Input mapping errors

**Solutions**:
```csharp
// Poll input events
while (window.PollEvents()) {
    switch (window.Event) {
        case KeyPressedEvent keyEvent:
            HandleKeyPress(keyEvent.Key);
            break;
        case MouseMovedEvent mouseEvent:
            HandleMouseMove(mouseEvent.Position);
            break;
    }
}

// Check window focus
if (window.IsFocused) {
    ProcessInput();
}
```

#### "Mouse sensitivity issues"
**Symptoms**: Mouse movement too fast/slow
**Causes**:
- Incorrect sensitivity scaling
- Delta time not applied
- Raw input not enabled

**Solutions**:
```csharp
// Apply sensitivity and delta time
float sensitivity = 0.1f;
Vector2 mouseDelta = GetMouseDelta();
Vector2 adjustedDelta = mouseDelta * sensitivity * deltaTime;

// Use raw input for consistent sensitivity
window.RawMouseMotion = true;
```

### 4. Camera Issues

#### "Camera not moving"
**Symptoms**: Camera doesn't respond to input
**Causes**:
- Input not connected to camera
- Camera update not called
- Matrix calculations incorrect

**Solutions**:
```csharp
// Update camera in game loop
public void Update(float deltaTime) {
    HandleInput(deltaTime);
    camera.Update(deltaTime);
}

// Check matrix calculations
public Matrix4 GetViewMatrix() {
    return Matrix4.LookAt(
        position,           // Camera position
        position + forward, // Look at position
        up                  // Up vector
    );
}
```

#### "Camera jitter"
**Symptoms**: Camera movement is jerky
**Causes**:
- Inconsistent delta time
- Input polling frequency
- Matrix precision issues

**Solutions**:
```csharp
// Smooth delta time
private float smoothDeltaTime;
private const float SMOOTH_FACTOR = 0.1f;

public void Update(float deltaTime) {
    smoothDeltaTime = Lerp(smoothDeltaTime, deltaTime, SMOOTH_FACTOR);
    camera.Update(smoothDeltaTime);
}

// Use consistent input polling
const float INPUT_POLL_RATE = 60f; // 60 times per second
float inputTimer = 0f;

public void Update(float deltaTime) {
    inputTimer += deltaTime;
    if (inputTimer >= 1f / INPUT_POLL_RATE) {
        PollInput();
        inputTimer = 0f;
    }
}
```

### 5. Voxel System Issues

#### "Voxel mesh not rendering"
**Symptoms**: Voxel world appears empty
**Causes**:
- Mesh generation failed
- Vertices not uploaded to GPU
- Shader not receiving data

**Solutions**:
```csharp
// Check mesh generation
public void GenerateMesh() {
    var vertices = new List<Vertex>();
    var indices = new List<uint>();
    
    // Generate mesh data
    for (int x = 0; x < CHUNK_SIZE; x++) {
        for (int y = 0; y < CHUNK_SIZE; y++) {
            for (int z = 0; z < CHUNK_SIZE; z++) {
                if (voxels[x, y, z] != 0) {
                    AddVoxelFaces(x, y, z, vertices, indices);
                }
            }
        }
    }
    
    // Upload to GPU
    if (vertices.Count > 0) {
        vertexBuffer.SetData(vertices.ToArray());
        indexBuffer.SetData(indices.ToArray());
    }
}

// Check shader inputs
glUniformMatrix4fv(viewMatrixLocation, 1, false, viewMatrix);
glUniformMatrix4fv(projectionMatrixLocation, 1, false, projectionMatrix);
```

#### "Chunk loading issues"
**Symptoms**: World doesn't load around player
**Causes**:
- Chunk loading not triggered
- Memory limits reached
- Loading queue full

**Solutions**:
```csharp
// Check chunk loading
public void UpdateChunks(Vector3 playerPosition) {
    var playerChunk = WorldToChunk(playerPosition);
    
    // Load nearby chunks
    for (int x = -LOAD_RADIUS; x <= LOAD_RADIUS; x++) {
        for (int z = -LOAD_RADIUS; z <= LOAD_RADIUS; z++) {
            var chunkCoord = playerChunk + new Vector3(x, 0, z);
            if (!IsChunkLoaded(chunkCoord)) {
                LoadChunk(chunkCoord);
            }
        }
    }
    
    // Unload distant chunks
    foreach (var chunk in loadedChunks) {
        if (Vector3.Distance(chunk.Key, playerChunk) > UNLOAD_RADIUS) {
            UnloadChunk(chunk.Key);
        }
    }
}
```

## 🔧 Debugging Techniques

### 1. Graphics Debugging

#### RenderDoc Integration
```csharp
// Enable RenderDoc capture
if (Environment.GetEnvironmentVariable("RENDERDOC_CAPTURE") == "1") {
    // RenderDoc is available
    RenderDoc.StartFrameCapture();
}

// Your rendering code here

if (Environment.GetEnvironmentVariable("RENDERDOC_CAPTURE") == "1") {
    RenderDoc.EndFrameCapture();
}
```

#### Debug Output
```csharp
// Enable debug output
GL.Enable(EnableCap.DebugOutput);
GL.DebugMessageCallback(DebugCallback, IntPtr.Zero);

private static void DebugCallback(DebugSource source, DebugType type, 
    int id, DebugSeverity severity, int length, IntPtr message, IntPtr userParam) {
    string messageStr = Marshal.PtrToStringAnsi(message, length);
    Console.WriteLine($"OpenGL Debug: {messageStr}");
}
```

### 2. Performance Profiling

#### Frame Time Profiling
```csharp
public class FrameProfiler {
    private Dictionary<string, float> timers = new Dictionary<string, float>();
    private Dictionary<string, float> averages = new Dictionary<string, float>();
    
    public void StartTimer(string name) {
        timers[name] = GetCurrentTime();
    }
    
    public void EndTimer(string name) {
        if (timers.ContainsKey(name)) {
            float elapsed = GetCurrentTime() - timers[name];
            UpdateAverage(name, elapsed);
            timers.Remove(name);
        }
    }
    
    private void UpdateAverage(string name, float value) {
        if (!averages.ContainsKey(name)) {
            averages[name] = value;
        } else {
            averages[name] = Lerp(averages[name], value, 0.1f);
        }
    }
}
```

#### Memory Profiling
```csharp
// Track memory usage
public class MemoryProfiler {
    public static void LogMemoryUsage(string context) {
        var process = Process.GetCurrentProcess();
        var memoryMB = process.WorkingSet64 / (1024 * 1024);
        Console.WriteLine($"{context}: {memoryMB}MB");
    }
    
    public static void ForceGC() {
        GC.Collect();
        GC.WaitForPendingFinalizers();
        GC.Collect();
    }
}
```

### 3. Input Debugging

#### Input Event Logging
```csharp
public class InputDebugger {
    private List<string> inputLog = new List<string>();
    
    public void LogInput(string input) {
        inputLog.Add($"{DateTime.Now:HH:mm:ss.fff}: {input}");
        
        // Keep only last 100 entries
        if (inputLog.Count > 100) {
            inputLog.RemoveAt(0);
        }
    }
    
    public void PrintInputLog() {
        foreach (var entry in inputLog) {
            Console.WriteLine(entry);
        }
    }
}
```

## 🚀 Performance Optimization

### 1. Rendering Optimization

#### Draw Call Batching
```csharp
// Batch similar objects
public class RenderBatch {
    private List<RenderObject> objects = new List<RenderObject>();
    
    public void AddObject(RenderObject obj) {
        objects.Add(obj);
    }
    
    public void Render() {
        // Sort by material/shader
        objects.Sort((a, b) => a.Material.CompareTo(b.Material));
        
        // Render in batches
        foreach (var group in objects.GroupBy(o => o.Material)) {
            group.Key.Bind();
            foreach (var obj in group) {
                obj.Render();
            }
        }
    }
}
```

#### Frustum Culling
```csharp
// Don't render objects outside camera view
public bool IsInFrustum(Vector3 position, float radius) {
    foreach (var plane in frustumPlanes) {
        float distance = Vector3.Dot(plane.Normal, position) + plane.Distance;
        if (distance < -radius) {
            return false; // Object is outside frustum
        }
    }
    return true;
}
```

### 2. Memory Optimization

#### Object Pooling
```csharp
public class GameObjectPool {
    private Queue<GameObject> pool = new Queue<GameObject>();
    private int maxSize = 100;
    
    public GameObject Get() {
        if (pool.Count > 0) {
            var obj = pool.Dequeue();
            obj.Reset();
            return obj;
        }
        return new GameObject();
    }
    
    public void Return(GameObject obj) {
        if (pool.Count < maxSize) {
            pool.Enqueue(obj);
        }
    }
}
```

#### Memory Streaming
```csharp
// Load/unload resources based on usage
public class ResourceStreamer {
    private Dictionary<string, Resource> loadedResources = new Dictionary<string, Resource>();
    private Dictionary<string, int> refCounts = new Dictionary<string, int>();
    
    public Resource Load(string path) {
        if (loadedResources.ContainsKey(path)) {
            refCounts[path]++;
            return loadedResources[path];
        }
        
        var resource = LoadFromDisk(path);
        loadedResources[path] = resource;
        refCounts[path] = 1;
        return resource;
    }
    
    public void Unload(string path) {
        if (refCounts.ContainsKey(path)) {
            refCounts[path]--;
            if (refCounts[path] <= 0) {
                loadedResources[path].Dispose();
                loadedResources.Remove(path);
                refCounts.Remove(path);
            }
        }
    }
}
```

## 🎯 Best Practices

### 1. Error Handling
- Always check for OpenGL errors
- Validate shader compilation
- Handle resource loading failures
- Use try-catch for critical operations

### 2. Performance Monitoring
- Profile regularly, not just when problems occur
- Set performance budgets
- Monitor memory usage
- Track frame time consistency

### 3. Debugging Tools
- Use graphics debugging tools (RenderDoc)
- Enable debug output
- Log important events
- Use breakpoints strategically

### 4. Code Organization
- Separate rendering from game logic
- Use consistent naming conventions
- Document complex algorithms
- Keep functions small and focused

---

**Still having issues? Check the [Common Patterns](common-patterns.md) for architectural solutions!**

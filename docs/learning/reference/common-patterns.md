# Common Patterns - Engine Architecture Patterns

**Navigation**: [BlockCore](../../README.md) > [Learning](../README.md) > [Reference](common-patterns.md)

Essential architectural patterns for BlockCore development, explained for enterprise developers.

## 🏗️ Core Architecture Patterns

### 1. Game Loop Pattern
**Purpose**: Continuous execution model for real-time games

**Enterprise Analogy**: Like a web server's request loop, but continuous

**Structure**:
```csharp
while (running) {
    float deltaTime = GetDeltaTime();
    Update(deltaTime);    // Process game logic
    Render();             // Draw to screen
    SwapBuffers();        // Present frame
}
```

**Key Components**:
- **Time Management**: Delta time for frame-rate independence
- **State Updates**: Game logic processing
- **Rendering**: Visual output generation
- **Input Handling**: User interaction processing

**Benefits**:
- Consistent frame rate
- Real-time responsiveness
- Predictable execution flow

### 2. Component System Pattern
**Purpose**: Flexible object composition without inheritance

**Enterprise Analogy**: Like dependency injection, but for game objects

**Structure**:
```csharp
public class Entity {
    private Dictionary<Type, IComponent> components;
    
    public T GetComponent<T>() where T : IComponent;
    public void AddComponent<T>(T component) where T : IComponent;
    public void RemoveComponent<T>() where T : IComponent;
}

public interface IComponent {
    void Update(float deltaTime);
}
```

**Key Components**:
- **Entity**: Container for components
- **Component**: Single responsibility behavior
- **System**: Processes components of specific type

**Benefits**:
- Flexible object composition
- Easy to add/remove behaviors
- Better performance than inheritance

### 3. Resource Management Pattern
**Purpose**: Efficient loading and caching of game assets

**Enterprise Analogy**: Like database connection pooling, but for assets

**Structure**:
```csharp
public class ResourceManager<T> {
    private Dictionary<string, T> cache;
    private Dictionary<string, int> refCounts;
    
    public T Load(string path);
    public void Unload(string path);
    public void UnloadUnused();
}
```

**Key Components**:
- **Cache**: In-memory storage of loaded assets
- **Reference Counting**: Track usage to prevent premature unloading
- **Lazy Loading**: Load assets only when needed
- **Hot Reloading**: Update assets without restart

**Benefits**:
- Memory efficiency
- Fast access to frequently used assets
- Easy asset updates during development

## 🎮 Game-Specific Patterns

### 4. Chunk System Pattern
**Purpose**: Manage infinite worlds with limited memory

**Enterprise Analogy**: Like database pagination, but for 3D space

**Structure**:
```csharp
public class ChunkManager {
    private Dictionary<ChunkCoord, Chunk> loadedChunks;
    private Queue<ChunkCoord> loadQueue;
    private Queue<ChunkCoord> unloadQueue;
    
    public void Update(Vector3 playerPosition);
    public Chunk GetChunk(ChunkCoord coord);
}
```

**Key Components**:
- **Chunk**: Fixed-size region of world data
- **Loading Queue**: Chunks to be loaded
- **Unloading Queue**: Chunks to be unloaded
- **Spatial Indexing**: Efficient chunk lookup

**Benefits**:
- Memory efficiency for large worlds
- Smooth world streaming
- Predictable memory usage

### 5. Event System Pattern
**Purpose**: Decoupled communication between game systems

**Enterprise Analogy**: Like message queues, but for game events

**Structure**:
```csharp
public class EventBus {
    private Dictionary<Type, List<IEventHandler>> handlers;
    
    public void Subscribe<T>(IEventHandler<T> handler);
    public void Unsubscribe<T>(IEventHandler<T> handler);
    public void Publish<T>(T event);
}
```

**Key Components**:
- **Event**: Data container for communication
- **Handler**: Processes specific event types
- **Bus**: Routes events to appropriate handlers

**Benefits**:
- Loose coupling between systems
- Easy to add new event types
- Centralized event routing

### 6. State Machine Pattern
**Purpose**: Manage complex game state transitions

**Enterprise Analogy**: Like workflow engines, but for game states

**Structure**:
```csharp
public class StateMachine<T> {
    private T currentState;
    private Dictionary<T, IState<T>> states;
    
    public void ChangeState(T newState);
    public void Update(float deltaTime);
}
```

**Key Components**:
- **State**: Current condition of system
- **Transition**: Rules for state changes
- **Action**: Behavior associated with states

**Benefits**:
- Clear state management
- Easy to debug state issues
- Predictable behavior

## ⚡ Performance Patterns

### 7. Object Pool Pattern
**Purpose**: Reuse objects to avoid garbage collection

**Enterprise Analogy**: Like connection pooling, but for game objects

**Structure**:
```csharp
public class ObjectPool<T> where T : new() {
    private Queue<T> pool;
    private Func<T> createFunc;
    
    public T Get();
    public void Return(T obj);
}
```

**Key Components**:
- **Pool**: Collection of reusable objects
- **Get**: Retrieve object from pool
- **Return**: Return object to pool
- **Reset**: Clear object state for reuse

**Benefits**:
- Reduced garbage collection
- Consistent performance
- Memory efficiency

### 8. Spatial Partitioning Pattern
**Purpose**: Efficient spatial queries in 3D space

**Enterprise Analogy**: Like database indexing, but for 3D coordinates

**Structure**:
```csharp
public class SpatialGrid {
    private Dictionary<GridCoord, List<ISpatialObject>> grid;
    private float cellSize;
    
    public List<ISpatialObject> Query(Vector3 position, float radius);
    public void Insert(ISpatialObject obj);
    public void Remove(ISpatialObject obj);
}
```

**Key Components**:
- **Grid**: 3D grid of cells
- **Cell**: Container for objects in specific region
- **Query**: Find objects in spatial region
- **Update**: Move objects between cells

**Benefits**:
- Efficient spatial queries
- Scalable to large numbers of objects
- Predictable performance

### 9. Command Pattern
**Purpose**: Encapsulate operations for undo/redo and queuing

**Enterprise Analogy**: Like command pattern in enterprise apps, but for game actions

**Structure**:
```csharp
public interface ICommand {
    void Execute();
    void Undo();
}

public class CommandManager {
    private Stack<ICommand> history;
    
    public void Execute(ICommand command);
    public void Undo();
    public void Redo();
}
```

**Key Components**:
- **Command**: Encapsulated operation
- **Invoker**: Executes commands
- **Receiver**: Performs actual operation
- **History**: Stack for undo/redo

**Benefits**:
- Undo/redo functionality
- Command queuing
- Decoupled execution

## 🔧 System Patterns

### 10. Plugin System Pattern
**Purpose**: Extensible architecture for third-party extensions

**Enterprise Analogy**: Like plugin architecture in enterprise apps

**Structure**:
```csharp
public interface IPlugin {
    string Name { get; }
    Version Version { get; }
    void Initialize(IPluginContext context);
    void Shutdown();
}

public class PluginManager {
    private List<IPlugin> loadedPlugins;
    
    public void LoadPlugin(string path);
    public void UnloadPlugin(string name);
    public T GetPlugin<T>() where T : IPlugin;
}
```

**Key Components**:
- **Plugin**: Extensible module
- **Manager**: Loads and manages plugins
- **Context**: Interface between plugin and engine
- **Sandbox**: Isolated execution environment

**Benefits**:
- Extensible architecture
- Third-party development
- Modular design

### 11. Factory Pattern
**Purpose**: Create objects without specifying exact classes

**Enterprise Analogy**: Like factory pattern in enterprise apps

**Structure**:
```csharp
public interface IGameObjectFactory {
    GameObject Create(string type, Vector3 position);
}

public class GameObjectFactory : IGameObjectFactory {
    private Dictionary<string, Func<GameObject>> creators;
    
    public GameObject Create(string type, Vector3 position) {
        return creators[type]();
    }
}
```

**Key Components**:
- **Factory**: Creates objects
- **Product**: Object being created
- **Creator**: Specific creation logic
- **Registry**: Maps types to creators

**Benefits**:
- Flexible object creation
- Easy to add new types
- Centralized creation logic

### 12. Observer Pattern
**Purpose**: Notify multiple objects of state changes

**Enterprise Analogy**: Like event handlers in enterprise apps

**Structure**:
```csharp
public interface IObserver<T> {
    void OnNotify(T data);
}

public class Observable<T> {
    private List<IObserver<T>> observers;
    
    public void Subscribe(IObserver<T> observer);
    public void Unsubscribe(IObserver<T> observer);
    public void Notify(T data);
}
```

**Key Components**:
- **Subject**: Object being observed
- **Observer**: Object receiving notifications
- **Notification**: Data about state change
- **Subscription**: Observer registration

**Benefits**:
- Loose coupling
- Easy to add/remove observers
- Centralized state management

## 🎯 When to Use Each Pattern

### Core Patterns (Always Use)
- **Game Loop**: Every game needs this
- **Component System**: For flexible object composition
- **Resource Management**: For asset loading

### Game-Specific Patterns (Use When Needed)
- **Chunk System**: For large worlds
- **Event System**: For decoupled communication
- **State Machine**: For complex state management

### Performance Patterns (Use for Optimization)
- **Object Pool**: For frequently created objects
- **Spatial Partitioning**: For many objects in 3D space
- **Command Pattern**: For undo/redo functionality

### System Patterns (Use for Architecture)
- **Plugin System**: For extensibility
- **Factory Pattern**: For flexible object creation
- **Observer Pattern**: For state notifications

## 🚀 Implementation Tips

### Start Simple
- Begin with basic patterns
- Add complexity gradually
- Refactor as needed

### Performance First
- Profile before optimizing
- Use appropriate patterns
- Measure impact

### Maintainability
- Keep patterns consistent
- Document architectural decisions
- Use clear naming

---

## 📖 Navigation

**Previous**: [Glossary](glossary.md)  
**Next**: [Troubleshooting](troubleshooting.md)

**Need help with specific patterns? Check the [Troubleshooting](troubleshooting.md) guide!**

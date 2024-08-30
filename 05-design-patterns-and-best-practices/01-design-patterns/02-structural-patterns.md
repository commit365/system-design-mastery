# 02. Structural Patterns

## Overview

Structural patterns are a category of design patterns that focus on how objects and classes are composed to form larger structures while ensuring flexibility and efficiency. These patterns help define the relationships between entities, promoting better organization and management of complex systems. This lesson will explore the key structural patterns, their characteristics, benefits, challenges, and examples of commonly used structural patterns in software development.

## What are Structural Patterns?

**Definition**: Structural patterns are design patterns that deal with the composition of classes and objects. They facilitate the creation of complex structures by defining how objects and classes can work together to achieve a common goal.

### Key Characteristics of Structural Patterns

1. **Composition**: Structural patterns emphasize the composition of objects, allowing for the creation of complex structures from simpler components.

2. **Flexibility**: These patterns promote flexibility by allowing objects to be composed in various ways, enabling easier changes and adaptations to the system.

3. **Encapsulation**: Structural patterns often encapsulate the details of how objects interact, providing a clear interface for clients to interact with the composed structure.

## Common Structural Patterns

### 1. Adapter Pattern

**Definition**: The Adapter pattern allows incompatible interfaces to work together by converting the interface of a class into another interface that clients expect.

#### Characteristics

- Acts as a bridge between two incompatible interfaces.
- Enables the integration of legacy code with new systems.

#### Benefits

- Promotes code reusability by allowing existing classes to be used in new contexts.
- Simplifies the integration of third-party libraries or components.

#### Challenges

- Can introduce additional complexity in the codebase.
- May lead to performance overhead if not implemented carefully.

#### Example

```python
class EuropeanSocket:
    def connect(self):
        return "Connected using European socket."

class AmericanSocket:
    def connect(self):
        return "Connected using American socket."

class SocketAdapter:
    def __init__(self, socket):
        self.socket = socket

    def connect(self):
        return self.socket.connect()

# Usage
euro_socket = EuropeanSocket()
adapter = SocketAdapter(euro_socket)
print(adapter.connect())  # Output: Connected using European socket.
```

### 2. Decorator Pattern

**Definition**: The Decorator pattern allows behavior to be added to individual objects dynamically without altering the structure of the objects.

#### Characteristics

- Provides a flexible alternative to subclassing for extending functionality.
- Supports the Single Responsibility Principle by allowing functionality to be divided among classes.

#### Benefits

- Enables the addition of new behavior without modifying existing code.
- Facilitates the creation of complex behaviors by combining multiple decorators.

#### Challenges

- Can lead to a large number of small classes, making the system harder to understand.
- Requires careful management of decorators to avoid excessive complexity.

#### Example

```python
class Coffee:
    def cost(self):
        return 5

class MilkDecorator:
    def __init__(self, coffee):
        self.coffee = coffee

    def cost(self):
        return self.coffee.cost() + 1

class SugarDecorator:
    def __init__(self, coffee):
        self.coffee = coffee

    def cost(self):
        return self.coffee.cost() + 0.5

# Usage
coffee = Coffee()
print(coffee.cost())  # Output: 5

milk_coffee = MilkDecorator(coffee)
print(milk_coffee.cost())  # Output: 6

sugar_milk_coffee = SugarDecorator(milk_coffee)
print(sugar_milk_coffee.cost())  # Output: 6.5
```

### 3. Facade Pattern

**Definition**: The Facade pattern provides a simplified interface to a complex subsystem, making it easier for clients to interact with the subsystem.

#### Characteristics

- Hides the complexities of the subsystem from the client.
- Provides a unified interface for interacting with multiple components.

#### Benefits

- Simplifies client interactions with complex systems.
- Reduces dependencies on the internal workings of the subsystem.

#### Challenges

- Can lead to a situation where the facade becomes a "God Object" if not designed carefully.
- May limit access to advanced features of the subsystem.

#### Example

```python
class CPU:
    def freeze(self):
        print("CPU frozen.")

    def jump(self, position):
        print(f"Jumping to {position}.")

    def execute(self):
        print("Executing.")

class Memory:
    def load(self, position, data):
        print(f"Loading data '{data}' at {position}.")

class HardDrive:
    def read(self, lba, size):
        return f"Data from LBA {lba} with size {size}"

class ComputerFacade:
    def __init__(self):
        self.cpu = CPU()
        self.memory = Memory()
        self.hard_drive = HardDrive()

    def start(self):
        self.cpu.freeze()
        self.memory.load(0, self.hard_drive.read(0, 1024))
        self.cpu.jump(0)
        self.cpu.execute()

# Usage
computer = ComputerFacade()
computer.start()
```

### 4. Composite Pattern

**Definition**: The Composite pattern allows clients to treat individual objects and compositions of objects uniformly. It is used to represent part-whole hierarchies.

#### Characteristics

- Composes objects into tree structures to represent hierarchies.
- Allows clients to work with complex structures in a uniform way.

#### Benefits

- Simplifies client code by allowing it to treat individual objects and composites uniformly.
- Encourages the use of recursive structures for representing hierarchies.

#### Challenges

- Can lead to a design that is overly general, making it harder to enforce restrictions on the components.
- May complicate the implementation of certain operations.

#### Example

```python
class Graphic:
    def draw(self):
        pass

class Circle(Graphic):
    def draw(self):
        print("Drawing a circle.")

class Square(Graphic):
    def draw(self):
        print("Drawing a square.")

class CompositeGraphic(Graphic):
    def __init__(self):
        self.graphics = []

    def add(self, graphic):
        self.graphics.append(graphic)

    def draw(self):
        for graphic in self.graphics:
            graphic.draw()

# Usage
circle = Circle()
square = Square()

composite = CompositeGraphic()
composite.add(circle)
composite.add(square)

composite.draw()  # Output: Drawing a circle. Drawing a square.
```

## Best Practices for Using Structural Patterns

1. **Understand the Problem Domain**: Before applying a structural pattern, ensure that you fully understand the problem domain and the relationships between the objects involved.

2. **Choose the Right Pattern**: Select the structural pattern that best fits the specific problem you are trying to solve, considering factors such as complexity, scalability, and maintainability.

3. **Keep It Simple**: Avoid unnecessary complexity by using structural patterns judiciously. Implement them only when they provide clear benefits.

4. **Document Your Choices**: Maintain documentation for the structural patterns used in your codebase, including the rationale for their selection and how they are implemented.

5. **Refactor When Necessary**: As your application evolves, revisit and refactor the use of structural patterns to ensure they continue to meet the needs of the system.

## Conclusion

Structural patterns are essential tools for managing the composition of objects in software design. By understanding the various structural patterns, their benefits, challenges, and best practices for implementation, developers can create more flexible, maintainable, and scalable systems. Leveraging structural patterns not only enhances code quality but also promotes collaboration and communication among development teams.

Next: [03. Behavioral Patterns](./03-behavioral-patterns.md)

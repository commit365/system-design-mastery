# 01. Creational Patterns

## Overview

Creational patterns are a category of design patterns that focus on the mechanisms of object creation. They provide various ways to create objects while hiding the creation logic, making the system more flexible and reusable. By using creational patterns, developers can manage object creation in a way that is appropriate for the situation, leading to improved code maintainability and scalability. This lesson will explore the key creational patterns, their characteristics, benefits, challenges, and examples.

## What are Creational Patterns?

**Definition**: Creational patterns are design patterns that deal with object creation mechanisms. They abstract the instantiation process, allowing the system to be independent of how its objects are created, composed, and represented.

### Key Characteristics of Creational Patterns

1. **Encapsulation of Object Creation**: Creational patterns encapsulate the logic of object creation, allowing for a more flexible and maintainable codebase.

2. **Control Over Object Creation**: These patterns provide control over the instantiation process, allowing developers to manage how and when objects are created.

3. **Flexibility and Reusability**: By abstracting the creation process, creational patterns promote flexibility and reusability, making it easier to modify or extend the system.

## Common Creational Patterns

### 1. Singleton Pattern

**Definition**: The Singleton pattern ensures that a class has only one instance and provides a global point of access to that instance.

#### Characteristics

- Guarantees that a class has a single instance.
- Provides a global access point to the instance.
- Lazy initialization can be implemented to create the instance only when it is needed.

#### Benefits

- Controlled access to a single instance.
- Reduced memory footprint since only one instance is created.
- Simplifies the management of shared resources.

#### Challenges

- Difficult to subclass.
- Can lead to issues in multi-threaded environments if not implemented correctly.

#### Example

```python
class Singleton:
    _instance = None

    def __new__(cls):
        if cls._instance is None:
            cls._instance = super(Singleton, cls).__new__(cls)
        return cls._instance

# Usage
singleton1 = Singleton()
singleton2 = Singleton()

assert singleton1 is singleton2  # Both variables point to the same instance
```

### 2. Factory Method Pattern

**Definition**: The Factory Method pattern defines an interface for creating objects but allows subclasses to alter the type of objects that will be created.

#### Characteristics

- Provides a way to delegate the instantiation process to subclasses.
- Promotes loose coupling by relying on interfaces rather than concrete classes.

#### Benefits

- Flexibility in object creation.
- Encourages adherence to the Open/Closed Principle, allowing for easy extension of the code.

#### Challenges

- Can lead to an increase in the number of classes in the system.
- Requires careful design to avoid overcomplicating the object creation process.

#### Example

```python
class Product:
    def operation(self):
        pass

class ConcreteProductA(Product):
    def operation(self):
        return "Result of ConcreteProductA"

class ConcreteProductB(Product):
    def operation(self):
        return "Result of ConcreteProductB"

class Creator:
    def factory_method(self):
        pass

class ConcreteCreatorA(Creator):
    def factory_method(self):
        return ConcreteProductA()

class ConcreteCreatorB(Creator):
    def factory_method(self):
        return ConcreteProductB()

# Usage
creator = ConcreteCreatorA()
product = creator.factory_method()
print(product.operation())  # Output: Result of ConcreteProductA
```

### 3. Abstract Factory Pattern

**Definition**: The Abstract Factory pattern provides an interface for creating families of related or dependent objects without specifying their concrete classes.

#### Characteristics

- Encapsulates a group of individual factories.
- Promotes the creation of products that are designed to work together.

#### Benefits

- Ensures that related products are created together.
- Facilitates the addition of new product families without altering existing code.

#### Challenges

- Can lead to a complex structure with many classes.
- Requires careful management of product families.

#### Example

```python
class AbstractProductA:
    def operation_a(self):
        pass

class AbstractProductB:
    def operation_b(self):
        pass

class ConcreteProductA1(AbstractProductA):
    def operation_a(self):
        return "Result of ConcreteProductA1"

class ConcreteProductA2(AbstractProductA):
    def operation_a(self):
        return "Result of ConcreteProductA2"

class ConcreteProductB1(AbstractProductB):
    def operation_b(self):
        return "Result of ConcreteProductB1"

class ConcreteProductB2(AbstractProductB):
    def operation_b(self):
        return "Result of ConcreteProductB2"

class AbstractFactory:
    def create_product_a(self):
        pass

    def create_product_b(self):
        pass

class ConcreteFactory1(AbstractFactory):
    def create_product_a(self):
        return ConcreteProductA1()

    def create_product_b(self):
        return ConcreteProductB1()

class ConcreteFactory2(AbstractFactory):
    def create_product_a(self):
        return ConcreteProductA2()

    def create_product_b(self):
        return ConcreteProductB2()

# Usage
factory = ConcreteFactory1()
product_a = factory.create_product_a()
product_b = factory.create_product_b()

print(product_a.operation_a())  # Output: Result of ConcreteProductA1
print(product_b.operation_b())  # Output: Result of ConcreteProductB1
```

### 4. Builder Pattern

**Definition**: The Builder pattern separates the construction of a complex object from its representation, allowing the same construction process to create different representations.

#### Characteristics

- Focuses on constructing a complex object step by step.
- Allows for the creation of different representations of an object.

#### Benefits

- Simplifies the creation of complex objects with many optional parameters.
- Promotes immutability by allowing objects to be built in a controlled manner.

#### Challenges

- Can introduce additional complexity in the codebase.
- Requires careful design to ensure that the builder is easy to use.

#### Example

```python
class Product:
    def __init__(self):
        self.parts = []

    def add(self, part):
        self.parts.append(part)

class Builder:
    def __init__(self):
        self.product = Product()

    def build_part_a(self):
        self.product.add("Part A")

    def build_part_b(self):
        self.product.add("Part B")

    def get_product(self):
        return self.product

# Usage
builder = Builder()
builder.build_part_a()
builder.build_part_b()
product = builder.get_product()

print(product.parts)  # Output: ['Part A', 'Part B']
```

## Best Practices for Using Creational Patterns

1. **Understand the Context**: Before applying a creational pattern, ensure that you fully understand the context and requirements of your application.

2. **Choose the Right Pattern**: Select the creational pattern that best fits the specific problem you are trying to solve, considering factors such as complexity, scalability, and maintainability.

3. **Keep It Simple**: Avoid unnecessary complexity by using creational patterns judiciously. Implement them only when they provide clear benefits.

4. **Document Your Choices**: Maintain documentation for the creational patterns used in your codebase, including the rationale for their selection and how they are implemented.

5. **Refactor When Necessary**: As your application evolves, revisit and refactor the use of creational patterns to ensure they continue to meet the needs of the system.

## Conclusion

Creational patterns are essential tools for managing object creation in software design. By understanding the various creational patterns, their benefits, challenges, and best practices for implementation, developers can create more flexible, maintainable, and scalable systems. Leveraging creational patterns not only enhances code quality but also promotes collaboration and communication among development teams.

Next: [02. Structural Patterns](./02-structural-patterns.md)

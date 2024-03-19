# Design Patterns & Principles
They are universally relevant architectural approaches. 

## Single Responsibility Principle
This principle states that a class should have only one reason to change, meaning it should have only one responsibility or job. By adhering to this principle, each class becomes focused and easier to understand, leading to better code organization and maintainability.

## Open/Closed Principle

The Open/Closed Principle states that software entities (classes, modules, functions, etc.) should be open for extension but closed for modification. In other words, you should be able to extend the behavior of a module without modifying its source code. This is typically achieved through abstractions, inheritance, and polymorphism.

## Liskov Substitution Principle

This principle emphasizes that objects of a superclass should be replaceable with objects of its subclass without affecting the program's correctness. In simpler terms, derived classes must be substitutable for their base classes without altering the program's desired properties. Violating this principle can lead to unexpected behavior in code that relies on polymorphism.

## Interface Segregation Principle

The Interface Segregation Principle suggests that clients should not be forced to depend on interfaces they do not use. Instead of creating large, monolithic interfaces, it's better to define more minor, more specific interfaces tailored to the needs of individual clients. This prevents the proliferation of unnecessary dependencies and makes systems easier to maintain and extend.

## Dependency Inversion Principle

The Dependency Inversion Principle advocates for high-level modules not to depend on low-level modules, but both should depend on abstractions. Additionally, it suggests that abstractions should not depend on details; instead, details should depend on abstractions. By adhering to this principle, you decouple components within a system, making it easier to replace or modify individual parts without affecting the entire system.

## <a id="builder"></a>[Builder Design Pattern](BUILDER.md)

## <a id="simple-factory"></a>[Simple Factory Pattern](SIMPLE-FACTORY.md)

## <a id="factory-method"></a>[Factory Method Pattern](FACTORY-METHOD.md)

## <a id="abstract-factory"></a>[Abstract Factory Pattern](ABSTRACT-FACTORY.md)

## <a id="prototype"></a>[Prototype Pattern](PROTOTYPE.md)

## <a id="singleton"></a>[Singleton Pattern](SINGLETON.md)

## <a id="bridge"></a>[Bridge Pattern](BRIDGE.md)

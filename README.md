# Design Patterns
Design patterns are common architectural approaches. They are universally relevant.

## Single Responsibility
This principle states that a class should have only one reason to change, meaning it should have only one responsibility or job. By adhering to this principle, each class becomes focused and easier to understand, leading to better code organization and maintainability.

## Open/Closed Principle

The Open/Closed Principle states that software entities (classes, modules, functions, etc.) should be open for extension but closed for modification. In other words, you should be able to extend the behavior of a module without modifying its source code. This is typically achieved through abstractions, inheritance, and polymorphism.

## Liskov Substitution Principle

This principle emphasizes that objects of a superclass should be replaceable with objects of its subclass without affecting the correctness of the program. In simpler terms, derived classes must be substitutable for their base classes without altering the desired properties of the program. Violating this principle can lead to unexpected behavior in code that relies on polymorphism.

## Interface Segregation Principle

The Interface Segregation Principle suggests that clients should not be forced to depend on interfaces they do not use. Instead of creating large, monolithic interfaces, it's better to define more minor, more specific interfaces tailored to the needs of individual clients. This prevents the proliferation of unnecessary dependencies and makes systems easier to maintain and extend.

## Dependency Inversion Principle

The Dependency Inversion Principle advocates for high-level modules not to depend on low-level modules, but both should depend on abstractions. Additionally, it suggests that abstractions should not depend on details; instead, details should depend on abstractions. By adhering to this principle, you decouple components within a system, making it easier to replace or modify individual parts without affecting the entire system.

## Builder Design Pattern

```csharp
using System;

// Product
class House
{
    public string Foundation { get; set; }
    public string Walls { get; set; }
    public string Roof { get; set; }
    public string Windows { get; set; }

    public void Display()
    {
        Console.WriteLine($"Foundation: {Foundation}, Walls: {Walls}, Roof: {Roof}, Windows: {Windows}");
    }
}

// Builder Interface
interface IHouseBuilder
{
    void BuildFoundation();
    void BuildWalls();
    void BuildRoof();
    void BuildWindows();
    House GetHouse();
}

// Concrete Builder
class SimpleHouseBuilder : IHouseBuilder
{
    private House house;

    public SimpleHouseBuilder()
    {
        house = new House();
    }

    public void BuildFoundation()
    {
        house.Foundation = "Concrete";
    }

    public void BuildWalls()
    {
        house.Walls = "Brick";
    }

    public void BuildRoof()
    {
        house.Roof = "Tiles";
    }

    public void BuildWindows()
    {
        house.Windows = "Glass";
    }

    public House GetHouse()
    {
        return house;
    }
}

// Director
class ConstructionEngineer
{
    private IHouseBuilder houseBuilder;

    public ConstructionEngineer(IHouseBuilder builder)
    {
        houseBuilder = builder;
    }

    public void ConstructHouse()
    {
        houseBuilder.BuildFoundation();
        houseBuilder.BuildWalls();
        houseBuilder.BuildRoof();
        houseBuilder.BuildWindows();
    }
}

class Program
{
    static void Main(string[] args)
    {
        SimpleHouseBuilder builder = new SimpleHouseBuilder();
        ConstructionEngineer engineer = new ConstructionEngineer(builder);

        engineer.ConstructHouse();

        House house = builder.GetHouse();
        Console.WriteLine("House Constructed:");
        house.Display();
    }
}

```

## SIMPLE FACTORY PATTERN

```csharp
using System;

public class VehicleFactory
{
    public static Vehicle CreateVehicle(string vehicleType)
    {
        switch (vehicleType)
        {
            case "car":
                return new Car();
            case "truck":
                return new Truck();
            default:
                throw new ArgumentException("Invalid vehicle type");
        }
    }
}

public abstract class Vehicle
{
    public abstract string Type { get; }
}

public class Car : Vehicle
{
    public override string Type => "Car";
}

public class Truck : Vehicle
{
    public override string Type => "Truck";
}

class Program
{
    static void Main(string[] args)
    {
        Vehicle vehicle1 = VehicleFactory.CreateVehicle("car");
        Console.WriteLine(vehicle1.Type); // Output: Car

        Vehicle vehicle2 = VehicleFactory.CreateVehicle("truck");
        Console.WriteLine(vehicle2.Type); // Output: Truck
    }
}
```

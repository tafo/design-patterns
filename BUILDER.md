## Builder Design Pattern

The Builder design pattern is a creational design pattern used to construct complex objects step by step. It separates the construction of a complex object from its representation, allowing the same construction process to create different representations of the object. It is also useful when creating an object with many optional parameters or configurations. It makes the code more readable and easier to maintain. Additionally, it allows flexibility and reusability in the construction process.

**Director** >>> This is responsible for orchestrating the construction process. It receives input from the client and delegates the construction steps to the builder.

**Builder** >>> This defines an abstract interface for creating parts of a complex object.

**Concrete Builders** >>> These are specific implementations of the Builder interface. They provide methods for building and retrieving the parts of the complex object.

**Product** >>> This is the complex object being constructed.

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

[Back](README.md/#builder)

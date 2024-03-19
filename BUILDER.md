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

[Back](README.md)

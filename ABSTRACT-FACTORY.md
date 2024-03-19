## Abstract Factory Design Pattern
```csharp
using System;

public abstract class VehicleFactory
{
    public abstract Car CreateCar();
    public abstract Truck CreateTruck();
}

public class FordFactory : VehicleFactory
{
    public override Car CreateCar()
    {
        return new FordCar();
    }

    public override Truck CreateTruck()
    {
        return new FordTruck();
    }
}

public class ChevroletFactory : VehicleFactory
{
    public override Car CreateCar()
    {
        return new ChevroletCar();
    }

    public override Truck CreateTruck()
    {
        return new ChevroletTruck();
    }
}

public abstract class Car { }
public abstract class Truck { }

public class FordCar : Car { }
public class ChevroletCar : Car { }

public class FordTruck : Truck { }
public class ChevroletTruck : Truck { }

class Program
{
    static void Main(string[] args)
    {
        VehicleFactory fordFactory = new FordFactory();
        Car car1 = fordFactory.CreateCar();
        Truck truck1 = fordFactory.CreateTruck();

        VehicleFactory chevroletFactory = new ChevroletFactory();
        Car car2 = chevroletFactory.CreateCar();
        Truck truck2 = chevroletFactory.CreateTruck();
    }
}
```
[Back](README.md/#abstract-facttory)

## SIMPLE FACTORY PATTERN

The Simple Factory Pattern, or the Static Factory Pattern, is a creational design pattern that provides a simple way to encapsulate the instantiation logic of objects within a single class or method, referred to as the "factory." This factory is responsible for creating objects based on the provided input parameters, such as strings, enums, or other data.

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
[Back](README.md/#simple-factory)

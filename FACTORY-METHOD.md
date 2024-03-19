## The Factory Method Design Pattern

The Factory Method Pattern is a creational design pattern used in software engineering. It defines an interface for creating objects but delegates the actual instantiation of objects to subclasses. Each subclass provides its implementation of the factory method, allowing it to create objects of a specific type.

```csharp

using System;

public abstract class Vehicle
{
    public abstract Vehicle CreateVehicle();
}

public class Car : Vehicle
{
    public override Vehicle CreateVehicle()
    {
        return new Car();
    }
}

public class Truck : Vehicle
{
    public override Vehicle CreateVehicle()
    {
        return new Truck();
    }
}

class Program
{
    static void Main(string[] args)
    {
        Vehicle carFactory = new Car();
        Vehicle vehicle1 = carFactory.CreateVehicle();
        Console.WriteLine(vehicle1.GetType().Name); // Output: Car

        Vehicle truckFactory = new Truck();
        Vehicle vehicle2 = truckFactory.CreateVehicle();
        Console.WriteLine(vehicle2.GetType().Name); // Output: Truck
    }
}

```
[Back](README.md/#factory-method)

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

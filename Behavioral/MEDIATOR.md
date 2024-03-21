## The Mediator Design Pattern

The Mediator Design Pattern is a behavioral design pattern that promotes loose coupling between objects by encapsulating how they interact and communicate with each other through a mediator object. It helps to centralize communication logic and reduces direct dependencies between objects, making the system more maintainable and flexible.

Mediator: This interface defines the communication interface between colleague objects. It typically contains methods for colleagues to send and receive messages.

Concrete Mediator: This class implements the mediator interface and coordinates the communication between colleague objects. It maintains references to all colleague objects and routes messages between them.

Colleague: These are the objects that communicate with each other through the mediator. They are aware of the mediator object but are not directly aware of each other.

```csharp
using System;
using System.Collections.Generic;

// Mediator interface
public interface ISmartHomeMediator
{
    void SendMessage(ISmartDevice sender, string message);
}

// Concrete mediator: SmartHomeHub
public class SmartHomeHub : ISmartHomeMediator
{
    public void SendMessage(ISmartDevice sender, string message)
    {
        Console.WriteLine($"Message from {sender.Name}: {message}");
    }
}

// Colleague: SmartDevice
public interface ISmartDevice
{
    string Name { get; }
    void SendMessage(string message);
}

// Concrete colleague: LightBulb
public class LightBulb : ISmartDevice
{
    public string Name { get; }

    public LightBulb(string name)
    {
        Name = name;
    }

    public void SendMessage(string message)
    {
        Console.WriteLine($"{Name}: Sending message - {message}");
        // Simulate sending message to smart home hub
        Mediator.SendMessage(this, message);
    }
}

// Concrete colleague: Thermostat
public class Thermostat : ISmartDevice
{
    public string Name { get; }

    public Thermostat(string name)
    {
        Name = name;
    }

    public void SendMessage(string message)
    {
        Console.WriteLine($"{Name}: Sending message - {message}");
        // Simulate sending message to smart home hub
        Mediator.SendMessage(this, message);
    }
}

// Client code
class Program
{
    static void Main(string[] args)
    {
        // Create smart home hub
        ISmartHomeMediator smartHomeHub = new SmartHomeHub();

        // Create smart devices
        ISmartDevice lightBulb = new LightBulb("Living Room Light");
        ISmartDevice thermostat = new Thermostat("Living Room Thermostat");

        // Set the mediator for smart devices
        SetMediator(lightBulb, smartHomeHub);
        SetMediator(thermostat, smartHomeHub);

        // Smart devices send messages
        lightBulb.SendMessage("Turn on the light");
        thermostat.SendMessage("Set temperature to 22°C");
    }

    static void SetMediator(ISmartDevice smartDevice, ISmartHomeMediator mediator)
    {
        // Set mediator for smart device
        // This method can be called during initialization or configuration of smart devices
        // to set the mediator they will use for communication.
        Mediator = mediator;
    }
}
```
[Back](../README.md#mediator)

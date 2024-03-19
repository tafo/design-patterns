## The Bridge Design Pattern

The Bridge Design Pattern is a structural design pattern that decouples an abstraction from its implementation so that the two can vary independently. It allows the abstraction and the implementation to change and evolve independently without affecting each other. This pattern is useful when there are multiple orthogonal dimensions of variation, such as different platforms, devices, or data sources.

### Abstraction
Define an abstraction interface or abstract class that represents the higher-level functionality. This interface contains methods that delegate to the implementation.

### Implementor
Define an implementor interface or abstract class that represents the lower-level implementation details. This interface contains methods that define the operations that can be performed.

### Concrete Implementor
Implement concrete classes that provide specific implementations of the implementor interface.

### Refined Abstraction
Define concrete classes that extend the abstraction interface and refine its behavior by providing additional functionality or customization.

```csharp
using System;

// Implementor interface
public interface IDevice
{
    void TurnOn();
    void TurnOff();
    void SetChannel(int channel);
    void SetVolume(int volume);
    void OpenMenu();
}

// Concrete Implementors: Device-Specific Implementations
public class TV : IDevice
{
    public void TurnOn()
    {
        Console.WriteLine("TV is turned on");
    }

    public void TurnOff()
    {
        Console.WriteLine("TV is turned off");
    }

    public void SetChannel(int channel)
    {
        Console.WriteLine($"Channel set to {channel} on TV");
    }

    public void SetVolume(int volume)
    {
        Console.WriteLine($"Volume set to {volume} on TV");
    }

    public void OpenMenu()
    {
        Console.WriteLine("Menu opened on TV");
    }
}

public class DVDPlayer : IDevice
{
    public void TurnOn()
    {
        Console.WriteLine("DVD Player is turned on");
    }

    public void TurnOff()
    {
        Console.WriteLine("DVD Player is turned off");
    }

    public void SetChannel(int channel)
    {
        Console.WriteLine("DVD Player does not have channel setting");
    }

    public void SetVolume(int volume)
    {
        Console.WriteLine("DVD Player does not have volume control");
    }

    public void OpenMenu()
    {
        Console.WriteLine("Menu opened on DVD Player");
    }
}

// Abstraction interface
public interface IRemoteControl
{
    void PowerOn();
    void PowerOff();
    void ChangeChannel(int channel);
    void AdjustVolume(int volume);
    void AccessMenu();
}

// Refined Abstraction: Remote Control
public class RemoteControl : IRemoteControl
{
    protected readonly IDevice device;

    public RemoteControl(IDevice device)
    {
        this.device = device;
    }

    public void PowerOn()
    {
        device.TurnOn();
    }

    public void PowerOff()
    {
        device.TurnOff();
    }

    public void ChangeChannel(int channel)
    {
        device.SetChannel(channel);
    }

    public void AdjustVolume(int volume)
    {
        device.SetVolume(volume);
    }

    public void AccessMenu()
    {
        device.OpenMenu();
    }
}

class Program
{
    static void Main(string[] args)
    {
        // Using the Remote Control with TV
        IDevice tv = new TV();
        IRemoteControl tvRemote = new RemoteControl(tv);

        tvRemote.PowerOn();             // Output: TV is turned on
        tvRemote.ChangeChannel(5);      // Output: Channel set to 5 on TV
        tvRemote.AdjustVolume(20);      // Output: Volume set to 20 on TV
        tvRemote.AccessMenu();          // Output: Menu opened on TV
        tvRemote.PowerOff();            // Output: TV is turned off

        Console.WriteLine();

        // Using the Remote Control with DVD Player
        IDevice dvdPlayer = new DVDPlayer();
        IRemoteControl dvdRemote = new RemoteControl(dvdPlayer);

        dvdRemote.PowerOn();            // Output: DVD Player is turned on
        dvdRemote.OpenMenu();           // Output: Menu opened on DVD Player
        dvdRemote.PowerOff();           // Output: DVD Player is turned off
    }
}
```
[Back](README.md/#bridge)

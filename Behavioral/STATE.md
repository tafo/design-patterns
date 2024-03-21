## The State Design Pattern

The State Design Pattern is a behavioral design pattern that allows an object to alter its behavior when its internal state changes. This pattern encapsulates the object's behavior in different states and allows the object to transition from one state to another at runtime without changing its class.

Context: This is the class that contains the state. It delegates state-specific behavior to different State objects and can have its state changed at runtime.

State: This is an interface or abstract class that defines a set of methods representing different states. Each concrete state class implements these methods to provide behavior specific to that state.

Concrete States: These are the concrete implementations of the State interface. Each concrete state class encapsulates behavior specific to a particular state of the context object.

```csharp
using System;
using System.Threading;

// Context class: TrafficLightController
public class TrafficLightController
{
    private ITrafficLightState _currentState;

    // Constructor to initialize the traffic light with a default state
    public TrafficLightController()
    {
        // Set the initial state to 'GreenState'
        _currentState = new GreenState(this);
    }

    // Setter for changing the current state
    public void SetState(ITrafficLightState state)
    {
        _currentState = state;
    }

    // Method to start the traffic light control system
    public void Start()
    {
        while (true)
        {
            // Let the current state handle the behavior
            _currentState.Handle();
            // Sleep for a short duration before switching states
            Thread.Sleep(2000);
        }
    }
}

// State interface: ITrafficLightState
public interface ITrafficLightState
{
    void Handle();
}

// Concrete state: GreenState
public class GreenState : ITrafficLightState
{
    private readonly TrafficLightController _controller;

    public GreenState(TrafficLightController controller)
    {
        _controller = controller;
    }

    public void Handle()
    {
        Console.WriteLine("Green light: Go!");
        // Transition to the next state after some time
        Thread.Sleep(5000);
        _controller.SetState(new YellowState(_controller));
    }
}

// Concrete state: YellowState
public class YellowState : ITrafficLightState
{
    private readonly TrafficLightController _controller;

    public YellowState(TrafficLightController controller)
    {
        _controller = controller;
    }

    public void Handle()
    {
        Console.WriteLine("Yellow light: Prepare to stop!");
        // Transition to the next state after some time
        Thread.Sleep(2000);
        _controller.SetState(new RedState(_controller));
    }
}

// Concrete state: RedState
public class RedState : ITrafficLightState
{
    private readonly TrafficLightController _controller;

    public RedState(TrafficLightController controller)
    {
        _controller = controller;
    }

    public void Handle()
    {
        Console.WriteLine("Red light: Stop!");
        // Transition to the next state after some time
        Thread.Sleep(3000);
        _controller.SetState(new GreenState(_controller));
    }
}

// Client code
class Program
{
    static void Main(string[] args)
    {
        // Create a traffic light controller instance
        TrafficLightController controller = new TrafficLightController();

        // Start the traffic light control system
        controller.Start();
    }
}
```
[Back](../README.md#state)

## The Facade Design Pattern

The Facade Design Pattern is a structural design pattern that provides a simplified interface to a complex system of classes, libraries, or APIs. It hides the complexities of the underlying system and provides a single entry point for interacting with it.

Facade: This is the main entry point of the pattern. It provides a unified interface to a set of interfaces in a subsystem. The facade delegates client requests to the appropriate objects in the subsystem.

Subsystems: These are a set of classes or components that perform the actual work. They encapsulate the complex functionality of the system. The facade delegates requests to these subsystems, but clients are shielded from the details of the subsystems.

```csharp
using System;

// Subsystem: DVD player
public class DVDPlayer
{
    public void Play()
    {
        Console.WriteLine("DVD is playing");
    }

    public void Stop()
    {
        Console.WriteLine("DVD stopped");
    }
}

// Subsystem: Projector
public class Projector
{
    public void TurnOn()
    {
        Console.WriteLine("Projector turned on");
    }

    public void TurnOff()
    {
        Console.WriteLine("Projector turned off");
    }
}

// Subsystem: Audio system
public class AudioSystem
{
    public void SetVolume(int volume)
    {
        Console.WriteLine($"Audio system volume set to {volume}");
    }
}

// Facade: Multimedia system controller
public class MultimediaFacade
{
    private readonly DVDPlayer dvdPlayer;
    private readonly Projector projector;
    private readonly AudioSystem audioSystem;

    public MultimediaFacade()
    {
        dvdPlayer = new DVDPlayer();
        projector = new Projector();
        audioSystem = new AudioSystem();
    }

    public void StartMovie()
    {
        Console.WriteLine("Starting the movie...");

        dvdPlayer.Play();
        projector.TurnOn();
        audioSystem.SetVolume(10); // Set volume to a default value

        Console.WriteLine("Movie started");
    }

    public void StopMovie()
    {
        Console.WriteLine("Stopping the movie...");

        dvdPlayer.Stop();
        projector.TurnOff();

        Console.WriteLine("Movie stopped");
    }
}

// Client code
class Program
{
    static void Main(string[] args)
    {
        // Create the multimedia facade
        MultimediaFacade multimediaFacade = new MultimediaFacade();

        // Start and stop the movie using the facade
        multimediaFacade.StartMovie();
        Console.WriteLine();
        multimediaFacade.StopMovie();
    }
}
```
[Back](../README.md/#facade)

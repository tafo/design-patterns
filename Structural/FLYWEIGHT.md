## The Flyweight Design Pattern

The Flyweight Design Pattern is a structural design pattern that aims to minimize memory usage or computational expenses by sharing as much as possible with similar objects. It is particularly useful when dealing with a large number of similar objects, which would otherwise consume a significant amount of memory if each object were to store its own data independently.

Flyweight Factory: This is responsible for creating and managing flyweight objects. It ensures that flyweight objects are shared and reused properly.

Flyweight: This is an interface or abstract class that represents the shared state and behavior of flyweight objects. Flyweight objects are typically immutable and stateless, and they store intrinsic (shared) state.

Concrete Flyweight: This is a concrete implementation of the Flyweight interface. It represents individual flyweight objects and stores extrinsic (unique) state, if any.

Client: This is the application code that uses flyweight objects. It typically interacts with the flyweight factory to obtain or use flyweight objects.

```csharp
using System;
using System.Collections.Generic;

// Flyweight: Font interface
public interface IFont
{
    void Print(string text);
}

// Concrete Flyweight: Shared font object
public class Font : IFont
{
    private readonly string name;
    private readonly int size;

    public Font(string name, int size)
    {
        this.name = name;
        this.size = size;
    }

    public void Print(string text)
    {
        Console.WriteLine($"Printing '{text}' with {name} ({size}pt)");
    }
}

// Flyweight Factory: Manages flyweight objects
public class FontFactory
{
    private readonly Dictionary<string, IFont> fonts = new Dictionary<string, IFont>();

    public IFont GetFont(string name, int size)
    {
        string key = $"{name}_{size}";
        if (!fonts.ContainsKey(key))
        {
            // If the font does not exist, create a new one and store it in the dictionary
            fonts[key] = new Font(name, size);
        }
        return fonts[key];
    }
}

// Client code
class Program
{
    static void Main(string[] args)
    {
        // Create a font factory
        FontFactory fontFactory = new FontFactory();

        // Get and use flyweight objects
        IFont arial10 = fontFactory.GetFont("Arial", 10);
        arial10.Print("Hello");

        IFont arial12 = fontFactory.GetFont("Arial", 12);
        arial12.Print("World");

        // Reusing the same flyweight object
        IFont arial10Again = fontFactory.GetFont("Arial", 10);
        arial10Again.Print("Flyweight");

        // Check if the same object is reused
        Console.WriteLine(arial10 == arial10Again); // Output: True
    }
}
```
[Back](../README.md/#flyweight)

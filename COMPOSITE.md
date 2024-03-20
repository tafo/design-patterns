## The Composite Design Pattern

The Composite Design Pattern is a structural design pattern that allows you to compose objects into tree structures to represent part-whole hierarchies. It lets clients treat individual objects and compositions of objects uniformly.

### Component
Define an interface or abstract class representing the common operations for both simple and composite objects.

### Leaf
Implement the Component interface for leaf objects. Leaf objects are the individual objects that do not have any children in the hierarchy.

### Composite
Implement the Component interface for composite objects. Composite objects can contain child components, which can be either leaf objects or other composite objects.

```csharp
using System;
using System.Collections.Generic;

// Component interface
public interface IUIComponent
{
    void Render();
}

// Leaf: Represents a simple UI component like a button or label
public class Button : IUIComponent
{
    private readonly string label;

    public Button(string label)
    {
        this.label = label;
    }

    public void Render()
    {
        Console.WriteLine($"Button: {label}");
    }
}

// Composite: Represents a container that can hold multiple UI components
public class Panel : IUIComponent
{
    private readonly List<IUIComponent> children = new List<IUIComponent>();

    public void AddComponent(IUIComponent component)
    {
        children.Add(component);
    }

    public void RemoveComponent(IUIComponent component)
    {
        children.Remove(component);
    }

    public void Render()
    {
        Console.WriteLine("Panel:");
        foreach (var child in children)
        {
            child.Render();
        }
    }
}

// Client code
class Program
{
    static void Main(string[] args)
    {
        // Create UI components
        Button button1 = new Button("Submit");
        Button button2 = new Button("Cancel");

        // Create a panel and add buttons to it
        Panel panel = new Panel();
        panel.AddComponent(button1);
        panel.AddComponent(button2);

        // Render the panel
        panel.Render();
    }
}
```
[Back](README.md/#composite)

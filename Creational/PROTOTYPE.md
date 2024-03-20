## Prototype Design Pattern

The Prototype design pattern is a creational design pattern that allows the creation of new objects based on existing objects, known as prototypes, through cloning. This pattern is useful when constructing a new instance, and it is more efficient to copy an existing instance rather than create it from scratch, especially when the initialization process is complex or resource-intensive.

**Prototype Interface/Abstract Class** >>> Define an interface or abstract class that declares a method for cloning itself. Concrete prototype classes will implement this method.

**Concrete Prototype Classes** >>> Create concrete classes that implement the prototype interface or extend the abstract class. These classes will override the clone method to provide their own implementation for copying the object.

**Client** >>> Create new objects by cloning the prototype object instead of directly instantiating them. This eliminates the need for clients to know the specific classes of objects they're creating.

The Prototype pattern helps achieve flexibility and reduces the coupling between clients and the classes they use for object creation. It also promotes code reusability by allowing the creation of new objects with minimal duplication of code.

```csharp
using System;

// Prototype interface
public interface IShape
{
    IShape Clone();
    void Draw();
}

// Concrete prototype class for Circle
public class Circle : IShape
{
    public int Radius { get; set; }
    public string Color { get; set; }

    public Circle(int radius, string color)
    {
        Radius = radius;
        Color = color;
    }

    public IShape Clone()
    {
        // Perform deep copy
        return (IShape)MemberwiseClone();
    }

    public void Draw()
    {
        Console.WriteLine($"Drawing a {Color} circle with radius {Radius}");
    }
}

// Concrete prototype class for Rectangle
public class Rectangle : IShape
{
    public int Width { get; set; }
    public int Height { get; set; }
    public string Color { get; set; }

    public Rectangle(int width, int height, string color)
    {
        Width = width;
        Height = height;
        Color = color;
    }

    public IShape Clone()
    {
        // Perform deep copy
        return (IShape)MemberwiseClone();
    }

    public void Draw()
    {
        Console.WriteLine($"Drawing a {Color} rectangle with width {Width} and height {Height}");
    }
}

// Client code
class Program
{
    static void Main(string[] args)
    {
        // Create prototypes
        Circle circlePrototype = new Circle(10, "red");
        Rectangle rectanglePrototype = new Rectangle(20, 30, "blue");

        // Clone and modify prototypes
        Circle clonedCircle = (Circle)circlePrototype.Clone();
        clonedCircle.Color = "green";
        clonedCircle.Draw();

        Rectangle clonedRectangle = (Rectangle)rectanglePrototype.Clone();
        clonedRectangle.Width = 25;
        clonedRectangle.Height = 35;
        clonedRectangle.Draw();
    }
}
```
[Back](../README.md/#prototype)

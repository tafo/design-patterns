## Prototype Design Pattern

using System;

public interface IShape
{
    IShape Clone();
    void Draw();
}

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
        return (IShape)MemberwiseClone();
    }

    public void Draw()
    {
        Console.WriteLine($"Drawing a {Color} circle with radius {Radius}");
    }
}

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
        return (IShape)MemberwiseClone();
    }

    public void Draw()
    {
        Console.WriteLine($"Drawing a {Color} rectangle with width {Width} and height {Height}");
    }
}

class Program
{
    static void Main(string[] args)
    {
        Circle circlePrototype = new Circle(10, "red");
        Rectangle rectanglePrototype = new Rectangle(20, 30, "blue");

        Circle clonedCircle = (Circle)circlePrototype.Clone();
        clonedCircle.Color = "green";
        clonedCircle.Draw();

        Rectangle clonedRectangle = (Rectangle)rectanglePrototype.Clone();
        clonedRectangle.Width = 25;
        clonedRectangle.Height = 35;
        clonedRectangle.Draw();
    }
}

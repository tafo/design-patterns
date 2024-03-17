# Design Patterns
Design patterns are common architectural approaches. They are universally relevant.

## Single Responsibility
This principle states that a class should have only one reason to change, meaning it should have only one responsibility or job. By adhering to this principle, each class becomes focused and easier to understand, leading to better code organization and maintainability.

```csharp
public class SingleResponsibility
{
    public class CustomerEntity
    {
        public int Id { get; set; }
        public string Firstname { get; set; } = default!;
        public string Lastname { get; set; } = default!;
        // Other properties
    }

    public class CustomerRepository
    {
        public void Save(CustomerEntity customer)
        {
            // Statements
        }

        public void Delete(CustomerEntity customer)
        {
            // Statements
        }
        
        // Other Methods
    }
}
```

## Open/Closed Principle

The Open/Closed Principle states that software entities (classes, modules, functions, etc.) should be open for extension but closed for modification. In other words, you should be able to extend the behavior of a module without modifying its source code. This is typically achieved through abstractions, inheritance, and polymorphism.

```csharp
public class OpenClosed
{
    private enum Color
    {
        Red,
        Green,
        Blue
    }

    private enum Size
    {
        Small,
        Medium,
        Large
    }

    private class Product(string name, Color color, Size size)
    {
        public string Name = name;
        public Color Color = color;
        public Size Size = size;
    }

    private class ProductFilter
    {
        public static IEnumerable<Product> FilterByColor(IEnumerable<Product> products, Color color)
        {
            return products.Where(p => p.Color == color);
        }
    }

    public class OldDemo
    {
        public void Main()
        {
            var apple = new Product("Apple", Color.Green, Size.Small);
            var tree = new Product("Tree", Color.Green, Size.Large);
            var house = new Product("House", Color.Blue, Size.Large);
            
            Product[] products = [apple, tree, house];
            
            var productFilter = new ProductFilter();
            var greenProducts = ProductFilter.FilterByColor(products, Color.Green);
            Console.WriteLine("{0}", greenProducts.Count());
        }
    }

    private interface ISpecification<T>
    {
        bool IsSatisfied(Product p);
    }

    private interface IFilter<T>
    {
        IEnumerable<T> Filter(IEnumerable<T> products, ISpecification<T> spec);
    }

    private class ColorSpecification(Color color) : ISpecification<Product>
    {
        public bool IsSatisfied(Product p)
        {
            return p.Color == color;
        }
    }

    private class SizeSpecification(Size size) : ISpecification<Product>
    {
        public bool IsSatisfied(Product p)
        {
            return p.Size == size;
        }
    }

    // combinator
    private class AndSpecification<T>(ISpecification<T> first, ISpecification<T> second) : ISpecification<T>
    {
        public bool IsSatisfied(Product p)
        {
            return first.IsSatisfied(p) && second.IsSatisfied(p);
        }
    }

    private class BetterFilter : IFilter<Product>
    {
        public IEnumerable<Product> Filter(IEnumerable<Product> products, ISpecification<Product> spec)
        {
            return products.Where(spec.IsSatisfied);
        }
    }
    
    public class NewDemo
    {
        public void Main()
        {
            var apple = new Product("Apple", Color.Green, Size.Small);
            var tree = new Product("Tree", Color.Green, Size.Large);
            var house = new Product("House", Color.Blue, Size.Large);
            
            Product[] products = [apple, tree, house];

            var betterFilter = new BetterFilter();
            var greenProducts = betterFilter.Filter(products, new ColorSpecification(Color.Green));
            var largeProducts = betterFilter.Filter(products, new SizeSpecification(Size.Large));
            var largeAndBlueProducts = betterFilter.Filter(products, new AndSpecification<Product>(new SizeSpecification(Size.Large), new ColorSpecification(Color.Blue)));
        }
    }
}
```

## Liskov Substitution Principle

This principle emphasizes that objects of a superclass should be replaceable with objects of its subclass without affecting the correctness of the program. In simpler terms, derived classes must be substitutable for their base classes without altering the desired properties of the program. Violating this principle can lead to unexpected behavior in code that relies on polymorphism.

```csharp
public class Shape
{
    public virtual double Area()
    {
        return 0;
    }
}

public class Rectangle : Shape
{
    public double Width { get; set; }
    public double Height { get; set; }

    public override double Area()
    {
        return Width * Height;
    }
}

public class Square : Rectangle
{
    public override double Area()
    {
        return Width * Width; // Or Height * Height, it's the same for a square
    }
}
```
```csharp
void SetDimensions(Rectangle rectangle, double width, double height)
{
    rectangle.Width = width;
    rectangle.Height = height;
}

```
```csharp

Square square = new Square();
SetDimensions(square, 5, 10);

```

```csharp
public interface IShape
{
    double Area();
}

public class Rectangle : IShape
{
    public double Width { get; set; }
    public double Height { get; set; }

    public double Area()
    {
        return Width * Height;
    }
}

public class Square : IShape
{
    public double SideLength { get; set; }

    public double Area()
    {
        return SideLength * SideLength;
    }
}

```
```csharp

void SetDimensions(IShape shape, double width, double height)
{
    // Check if the shape is a rectangle
    if (shape is Rectangle rectangle)
    {
        rectangle.Width = width;
        rectangle.Height = height;
    }
    // Check if the shape is a square
    else if (shape is Square square)
    {
        square.SideLength = Math.Max(width, height); // Side length is the maximum of width or height for a square
    }
}

```


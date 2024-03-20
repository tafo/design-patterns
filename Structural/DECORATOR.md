## The Decorator Design Pattern

The Decorator Design Pattern is a structural design pattern that allows behavior to be added to individual objects, either statically or dynamically, without affecting the behavior of other objects from the same class. It is used to extend or alter the functionality of objects at runtime by wrapping them with additional behavior.

### Component
Define an interface or abstract class representing the base object that can be decorated.

### Concrete Component
Implement the Component interface to define the base object that can be decorated.

### Decorator
Implement the Component interface and maintain a reference to an object of the same interface. This allows the decorator to add additional behavior to the base object.

### Concrete Decorator
Extend the Decorator class to add specific behavior or modify existing behavior.

```csharp
using System;

// Component interface
public interface ICoffee
{
    string GetDescription();
    double GetCost();
}

// Concrete Component: Base coffee
public class SimpleCoffee : ICoffee
{
    public string GetDescription()
    {
        return "Simple Coffee";
    }

    public double GetCost()
    {
        return 1.0; // Base cost of simple coffee
    }
}

// Decorator: Abstract class for decorators
public abstract class CoffeeDecorator : ICoffee
{
    protected ICoffee decoratedCoffee;

    public CoffeeDecorator(ICoffee coffee)
    {
        this.decoratedCoffee = coffee;
    }

    public virtual string GetDescription()
    {
        return decoratedCoffee.GetDescription();
    }

    public virtual double GetCost()
    {
        return decoratedCoffee.GetCost();
    }
}

// Concrete Decorator: Milk
public class MilkDecorator : CoffeeDecorator
{
    public MilkDecorator(ICoffee coffee) : base(coffee)
    {
    }

    public override string GetDescription()
    {
        return $"{base.GetDescription()}, Milk";
    }

    public override double GetCost()
    {
        return base.GetCost() + 0.5; // Additional cost for milk
    }
}

// Concrete Decorator: Sugar
public class SugarDecorator : CoffeeDecorator
{
    public SugarDecorator(ICoffee coffee) : base(coffee)
    {
    }

    public override string GetDescription()
    {
        return $"{base.GetDescription()}, Sugar";
    }

    public override double GetCost()
    {
        return base.GetCost() + 0.2; // Additional cost for sugar
    }
}

class Program
{
    static void Main(string[] args)
    {
        // Create a base coffee
        ICoffee simpleCoffee = new SimpleCoffee();

        // Add milk to the base coffee
        ICoffee coffeeWithMilk = new MilkDecorator(simpleCoffee);
        Console.WriteLine($"Description: {coffeeWithMilk.GetDescription()}, Cost: ${coffeeWithMilk.GetCost()}");

        // Add sugar to the base coffee
        ICoffee coffeeWithMilkAndSugar = new SugarDecorator(coffeeWithMilk);
        Console.WriteLine($"Description: {coffeeWithMilkAndSugar.GetDescription()}, Cost: ${coffeeWithMilkAndSugar.GetCost()}");
    }
}
```
[Back](../README.md/#decorator)

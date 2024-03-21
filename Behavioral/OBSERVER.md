## The Observer Design Pattern

The Observer Design Pattern is a behavioral design pattern that establishes a one-to-many dependency relationship between objects, such that when one object (the subject or observable) changes its state, all its dependents (observers) are notified and updated automatically. This pattern is commonly used to implement distributed event handling systems, where changes in one part of the system need to be propagated to other parts.

Subject (Observable): This is the object that is being observed. It maintains a list of observers and provides methods to attach, detach, and notify observers of changes to its state.

Observer: This is the interface or abstract class defining the method(s) that the subject calls to notify the observer of changes.

Concrete Subject: This is the concrete implementation of the subject. It maintains the state and sends notifications to observers when the state changes.

Concrete Observer: This is the concrete implementation of the observer. It registers with the subject to receive notifications and updates its state accordingly.

```csharp
using System;
using System.Collections.Generic;

// Subject interface: IStock
public interface IStock
{
    string Symbol { get; }
    double Price { get; set; }
    void Attach(IObserver observer);
    void Detach(IObserver observer);
    void Notify();
}

// Concrete Subject: Stock
public class Stock : IStock
{
    private readonly List<IObserver> _observers = new List<IObserver>();

    public string Symbol { get; }
    private double _price;

    public double Price
    {
        get { return _price; }
        set
        {
            _price = value;
            Notify(); // Notify observers when price changes
        }
    }

    public Stock(string symbol, double price)
    {
        Symbol = symbol;
        Price = price;
    }

    public void Attach(IObserver observer)
    {
        _observers.Add(observer);
    }

    public void Detach(IObserver observer)
    {
        _observers.Remove(observer);
    }

    public void Notify()
    {
        foreach (var observer in _observers)
        {
            observer.Update(this); // Notify each observer
        }
    }
}

// Observer interface: IObserver
public interface IObserver
{
    void Update(IStock stock);
}

// Concrete Observer: Investor
public class Investor : IObserver
{
    private readonly string _name;

    public Investor(string name)
    {
        _name = name;
    }

    public void Update(IStock stock)
    {
        Console.WriteLine($"{_name} received notification: {stock.Symbol} price changed to {stock.Price}");
    }
}

// Client code
class Program
{
    static void Main(string[] args)
    {
        // Create stock instances
        Stock appleStock = new Stock("AAPL", 150.50);
        Stock googleStock = new Stock("GOOGL", 2800.75);

        // Create investors (observers)
        IObserver investor1 = new Investor("Alice");
        IObserver investor2 = new Investor("Bob");

        // Investors subscribe to stocks
        appleStock.Attach(investor1);
        appleStock.Attach(investor2);
        googleStock.Attach(investor2);

        // Simulate stock price changes
        appleStock.Price = 152.25;
        googleStock.Price = 2825.50;
    }
}
```
[Back](../README.md#observer)

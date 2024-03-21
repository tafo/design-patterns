## The Strategy Design Pattern

The Strategy Design Pattern is a behavioral design pattern that defines a family of algorithms, encapsulates each one, and makes them interchangeable. This pattern allows the algorithm to vary independently of the clients that use it, providing a way to select a specific algorithm at runtime.

Strategy: This is an interface or abstract class that defines a set of methods that represent different algorithms or strategies.

Concrete Strategies: These are the concrete implementations of the strategies defined in the Strategy interface.

Context: This is a class that maintains a reference to a Strategy object and delegates the algorithm to this object. The Context class allows clients to interact with different strategies without knowing their specific implementations.

```csharp
using System;

// Strategy interface
public interface IPaymentStrategy
{
    void ProcessPayment(double amount);
}

// Concrete strategy: CreditCardPayment
public class CreditCardPayment : IPaymentStrategy
{
    public void ProcessPayment(double amount)
    {
        Console.WriteLine($"Processing credit card payment of ${amount}");
        // Logic for processing credit card payment
    }
}

// Concrete strategy: PayPalPayment
public class PayPalPayment : IPaymentStrategy
{
    public void ProcessPayment(double amount)
    {
        Console.WriteLine($"Processing PayPal payment of ${amount}");
        // Logic for processing PayPal payment
    }
}

// Concrete strategy: BankTransferPayment
public class BankTransferPayment : IPaymentStrategy
{
    public void ProcessPayment(double amount)
    {
        Console.WriteLine($"Processing bank transfer payment of ${amount}");
        // Logic for processing bank transfer payment
    }
}

// Context class
public class PaymentProcessor
{
    private IPaymentStrategy _paymentStrategy;

    // Setter for the payment strategy
    public void SetPaymentStrategy(IPaymentStrategy paymentStrategy)
    {
        _paymentStrategy = paymentStrategy;
    }

    // Method to perform payment processing using the selected strategy
    public void ProcessPayment(double amount)
    {
        if (_paymentStrategy == null)
        {
            throw new InvalidOperationException("Payment strategy is not set");
        }

        _paymentStrategy.ProcessPayment(amount);
    }
}

// Client code
class Program
{
    static void Main(string[] args)
    {
        PaymentProcessor paymentProcessor = new PaymentProcessor();

        // Process payment using credit card
        paymentProcessor.SetPaymentStrategy(new CreditCardPayment());
        paymentProcessor.ProcessPayment(100.50);

        // Process payment using PayPal
        paymentProcessor.SetPaymentStrategy(new PayPalPayment());
        paymentProcessor.ProcessPayment(75.25);

        // Process payment using bank transfer
        paymentProcessor.SetPaymentStrategy(new BankTransferPayment());
        paymentProcessor.ProcessPayment(200.75);
    }
}
```
[Back](../README.md#strategy)

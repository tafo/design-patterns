## Singleton Design Pattern

The Singleton Design Pattern is a creational design pattern in computer science that ensures a class has only one instance and provides a global point of access to that instance throughout the application's lifecycle. This pattern is useful when exactly one object is needed to coordinate actions across the system, such as managing shared resources or maintaining a centralized configuration.

**Singleton Class**
Define a class that contains a private constructor to prevent instantiation from external classes. The class also provides a static method to access the singleton instance.

**Private Static Instance**
Declare a private static member variable within the class to hold the singleton instance.

**Initialization**
Lazily initialize the singleton instance within the class, either upon first access or eagerly during class loading.

**Singleton Access Method**
Implement a static method within the class to provide access to the singleton instance. This method ensures that only one instance of the class is created and returned to clients.

The Singleton pattern also helps improve performance and resource utilization by avoiding the overhead of creating multiple instances of the same class. Additionally, it promotes encapsulation by hiding the creation and management of the singleton instance within the class itself, reducing coupling between clients and the singleton class.

```csharp
public class Singleton
{
    // Private static instance variable
    private static Singleton instance;

    // Private constructor to prevent instantiation from external classes
    private Singleton() { }

    // Lazily initialize the singleton instance upon first access
    public static Singleton GetInstance()
    {
        // Check if the instance is null
        if (instance == null)
        {
            // If null, create a new instance
            instance = new Singleton();
        }
        
        // Return the singleton instance
        return instance;
    }

    // Example method of the singleton class
    public void PrintMessage()
    {
        Console.WriteLine("This is a Singleton instance.");
    }
}

class Program
{
    static void Main(string[] args)
    {
        // Access the singleton instance
        Singleton singleton = Singleton.GetInstance();

        // Call a method on the singleton instance
        singleton.PrintMessage();
    }
}
```
[Back](../README.md/#singleton)

## The Proxy Design Pattern

The Proxy Design Pattern is a structural design pattern that provides a placeholder for another object to control access to it. It allows you to create a substitute for an object to control access to it, add additional functionality, or perform some pre-processing and post-processing tasks before and after the core object's methods are invoked.

Subject Interface: Define an interface that both the real object (subject) and the proxy will implement. This allows the proxy to be used wherever the subject is expected.

Real Subject: Implement the actual object that the proxy represents. This is the object for which the proxy provides controlled access.

Proxy: Implement an object that acts as a surrogate for the real subject. The proxy has the same interface as the real subject so that clients can interact with it in the same way.

```csharp
using System;

// Subject Interface
public interface IFileManager
{
    void RequestFile(string fileName);
}

// Real Subject
public class FileManager : IFileManager
{
    public void RequestFile(string fileName)
    {
        Console.WriteLine($"File '{fileName}' requested from the network file system.");
    }
}

// Proxy
public class FileManagerProxy : IFileManager
{
    private readonly FileManager fileManager;
    private readonly string[] authorizedUsers = { "user1", "user2", "user3" };

    public FileManagerProxy()
    {
        fileManager = new FileManager();
    }

    public void RequestFile(string fileName)
    {
        // Perform authentication or access control before allowing access
        if (IsUserAuthorized())
        {
            fileManager.RequestFile(fileName);
        }
        else
        {
            Console.WriteLine($"Access to file '{fileName}' is not authorized.");
        }
    }

    private bool IsUserAuthorized()
    {
        // Simulated authentication logic
        string currentUser = "user2"; // Assume current user
        foreach (var user in authorizedUsers)
        {
            if (currentUser == user)
            {
                return true;
            }
        }
        return false;
    }
}

// Client code
class Program
{
    static void Main(string[] args)
    {
        // Use the proxy to request a file
        IFileManager fileManagerProxy = new FileManagerProxy();
        fileManagerProxy.RequestFile("document.txt"); // Access granted for user2

        // Simulate access for an unauthorized user
        fileManagerProxy.RequestFile("confidential.doc"); // Access denied for user2
    }
}
```
[Back](../README.md/#proxy)

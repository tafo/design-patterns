## The Chain of Responsibility Design Pattern

The Chain of Responsibility Design Pattern is a behavioral design pattern in which a request is passed through a chain of handlers, with each handler deciding either to process the request or to pass it to the next handler in the chain. This pattern decouples senders and receivers of a request based on the type of request and allows multiple objects to handle the request without explicitly specifying the receiver.

Handler Interface: Define an interface for handling requests. This interface usually includes a method for handling requests and a reference to the next handler in the chain.

Concrete Handlers: Implement the Handler interface to handle specific types of requests. Each concrete handler decides whether to handle the request or pass it to the next handler in the chain.

Client: Initiates requests and forwards them to the first handler in the chain.

```csharp
using System;

// Handler interface
public interface ILogHandler
{
    void SetNextHandler(ILogHandler handler);
    void HandleLog(LogMessage message);
}

// Concrete handler: ConsoleLogHandler
public class ConsoleLogHandler : ILogHandler
{
    private ILogHandler nextHandler;

    public void SetNextHandler(ILogHandler handler)
    {
        nextHandler = handler;
    }

    public void HandleLog(LogMessage message)
    {
        if (message.Severity == LogLevel.Info)
        {
            Console.WriteLine($"[Info] {message.Text}");
        }
        else if (nextHandler != null)
        {
            nextHandler.HandleLog(message); // Pass to the next handler
        }
    }
}

// Concrete handler: FileLogHandler
public class FileLogHandler : ILogHandler
{
    private ILogHandler nextHandler;

    public void SetNextHandler(ILogHandler handler)
    {
        nextHandler = handler;
    }

    public void HandleLog(LogMessage message)
    {
        if (message.Severity == LogLevel.Error || message.Severity == LogLevel.Warning)
        {
            Console.WriteLine($"[File] {message.Text}");
        }
        else if (nextHandler != null)
        {
            nextHandler.HandleLog(message); // Pass to the next handler
        }
    }
}

// Log message class
public class LogMessage
{
    public string Text { get; }
    public LogLevel Severity { get; }

    public LogMessage(string text, LogLevel severity)
    {
        Text = text;
        Severity = severity;
    }
}

// Log levels enum
public enum LogLevel
{
    Info,
    Warning,
    Error
}

// Logger class
public class Logger
{
    private ILogHandler logHandler;

    public Logger(ILogHandler logHandler)
    {
        this.logHandler = logHandler;
    }

    public void LogMessage(string text, LogLevel severity)
    {
        LogMessage message = new LogMessage(text, severity);
        logHandler.HandleLog(message);
    }
}

// Client code
class Program
{
    static void Main(string[] args)
    {
        // Create log handlers
        ILogHandler consoleHandler = new ConsoleLogHandler();
        ILogHandler fileHandler = new FileLogHandler();

        // Set up the chain of responsibility
        consoleHandler.SetNextHandler(fileHandler);

        // Create a logger with the console handler as the starting point
        Logger logger = new Logger(consoleHandler);

        // Log messages with different severity levels
        logger.LogMessage("This is an info message", LogLevel.Info);
        logger.LogMessage("This is a warning message", LogLevel.Warning);
        logger.LogMessage("This is an error message", LogLevel.Error);
    }
}
```
[Back](../README.md#chain)

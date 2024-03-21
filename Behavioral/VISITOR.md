## The Visitor Pattern 

The Visitor Design Pattern is a behavioral design pattern that allows you to separate algorithms from the objects on which they operate. It enables you to add new operations to existing classes without modifying them, promoting open/closed principle.

In the Visitor pattern, we define new operations in a separate visitor interface and provide implementations for these operations in concrete visitor classes. These visitor classes can then visit objects of various types, allowing us to perform different operations on these objects without changing their structure.

Visitor Interface: This interface declares a visit method for each class of element in the object structure. Each visit method accepts an element as a parameter and defines the operation to be performed on that element.

Concrete Visitor Classes: These are the implementations of the visitor interface. Each concrete visitor class provides a specific implementation for the visit method corresponding to a particular element class.

Element Interface: This interface declares an accept method that accepts a visitor as a parameter. This method is implemented by element classes to allow visitors to visit them.

Concrete Element Classes: These are the classes representing elements in the object structure. They implement the element interface and provide an implementation for the accept method.

```csharp
using System;
using System.Collections.Generic;

// Visitor interface
public interface IVisitor
{
    void Visit(Paragraph paragraph);
    void Visit(Heading heading);
    void Visit(Image image);
}

// Concrete visitor: SpellChecker
public class SpellChecker : IVisitor
{
    public void Visit(Paragraph paragraph)
    {
        Console.WriteLine($"Spell checking paragraph: {paragraph.Text}");
    }

    public void Visit(Heading heading)
    {
        Console.WriteLine($"Spell checking heading: {heading.Text}");
    }

    public void Visit(Image image)
    {
        // No spell checking for images
    }
}

// Concrete visitor: HtmlExporter
public class HtmlExporter : IVisitor
{
    public void Visit(Paragraph paragraph)
    {
        Console.WriteLine($"Exporting paragraph to HTML: <p>{paragraph.Text}</p>");
    }

    public void Visit(Heading heading)
    {
        Console.WriteLine($"Exporting heading to HTML: <h1>{heading.Text}</h1>");
    }

    public void Visit(Image image)
    {
        Console.WriteLine($"Exporting image to HTML: <img src=\"{image.Url}\" alt=\"{image.Description}\">");
    }
}

// Element interface
public interface IElement
{
    void Accept(IVisitor visitor);
}

// Concrete elements
public class Paragraph : IElement
{
    public string Text { get; }

    public Paragraph(string text)
    {
        Text = text;
    }

    public void Accept(IVisitor visitor)
    {
        visitor.Visit(this);
    }
}

public class Heading : IElement
{
    public string Text { get; }

    public Heading(string text)
    {
        Text = text;
    }

    public void Accept(IVisitor visitor)
    {
        visitor.Visit(this);
    }
}

public class Image : IElement
{
    public string Url { get; }
    public string Description { get; }

    public Image(string url, string description)
    {
        Url = url;
        Description = description;
    }

    public void Accept(IVisitor visitor)
    {
        visitor.Visit(this);
    }
}

// Client code
class Program
{
    static void Main(string[] args)
    {
        List<IElement> document = new List<IElement>
        {
            new Heading("Visitor Pattern Example"),
            new Paragraph("The Visitor pattern separates algorithms from the objects on which they operate."),
            new Image("image.jpg", "Sample Image")
        };

        // Spell check the document
        IVisitor spellChecker = new SpellChecker();
        foreach (var element in document)
        {
            element.Accept(spellChecker);
        }

        Console.WriteLine();

        // Export the document to HTML
        IVisitor htmlExporter = new HtmlExporter();
        foreach (var element in document)
        {
            element.Accept(htmlExporter);
        }
    }
}
```
[Back](../README.md/#visitor)

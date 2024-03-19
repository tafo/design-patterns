## The Adapter Design Pattern

The Adapter Design Pattern is a structural design pattern that allows incompatible interfaces of classes to work together. It acts as a bridge between two incompatible interfaces, enabling them to collaborate and interact seamlessly.

Here's how the Adapter pattern typically works:

### Target Interface
Define the interface that the client expects to work with. This is the interface that the client code is designed to use.

### Adaptee
Define the interface that needs to be adapted to work with the target interface. This is the interface that the client code cannot use directly.

### Adapter
Implement the adapter class that adapts the Adaptee interface to the Target interface. The adapter class contains an instance of the Adaptee and implements the Target interface by delegating the calls to the Adaptee.

```csharp
using System;
using System.Xml;

// Adaptee: Legacy system providing data in XML format
public class LegacyDataSystem
{
    public string GetDataAsXml()
    {
        // Simulate fetching data from the legacy system in XML format
        return "<data><name>Tayfun</name><age>41</age></data>";
    }
}

// Target Interface: New system requires data in JSON format
public interface IDataConverter
{
    string ConvertDataToJson();
}

// Adapter: Adapter to convert data from XML to JSON format
public class DataAdapter : IDataConverter
{
    private readonly LegacyDataSystem legacyDataSystem;

    public DataAdapter(LegacyDataSystem legacyDataSystem)
    {
        this.legacyDataSystem = legacyDataSystem;
    }

    public string ConvertDataToJson()
    {
        // Get data from legacy system in XML format
        string xmlData = legacyDataSystem.GetDataAsXml();

        // Convert XML to JSON (simplified conversion for demonstration)
        // In a real-world scenario, a proper XML to JSON conversion logic would be implemented
        string jsonData = $"{{ \"name\": \"{GetNameFromXml(xmlData)}\", \"age\": {GetAgeFromXml(xmlData)} }}";

        return jsonData;
    }

    private string GetNameFromXml(string xmlData)
    {
        // Extract name from XML (simplified extraction for demonstration)
        XmlDocument doc = new XmlDocument();
        doc.LoadXml(xmlData);
        return doc.SelectSingleNode("/data/name").InnerText;
    }

    private int GetAgeFromXml(string xmlData)
    {
        // Extract age from XML (simplified extraction for demonstration)
        XmlDocument doc = new XmlDocument();
        doc.LoadXml(xmlData);
        return int.Parse(doc.SelectSingleNode("/data/age").InnerText);
    }
}

// Client code: New system consuming data in JSON format
class Program
{
    static void Main(string[] args)
    {
        // Create an instance of the legacy data system
        LegacyDataSystem legacyDataSystem = new LegacyDataSystem();

        // Create an adapter to convert data from XML to JSON format
        IDataConverter dataAdapter = new DataAdapter(legacyDataSystem);

        // Convert data from XML to JSON format
        string jsonData = dataAdapter.ConvertDataToJson();

        // Output the converted JSON data
        Console.WriteLine("Converted JSON data:");
        Console.WriteLine(jsonData);
    }
}
```
[Back](README.md/#adapter)

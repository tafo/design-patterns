# Design Patterns
Design patterns are common architectural approaches. They are universally relevant.

## Single Responsibility
The Single Responsibility Principle states that a class should have only one reason to change. In other words, a class should have only one responsibility or job. If we adhere to the Single Responsibility Principle, 

1. We will have classes and modules that are easy to understand
2. We promote encapsulation, reusability, and testability
3. Maintenance becomes easier

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

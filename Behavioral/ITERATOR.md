## The Iterator Design Pattern

The Iterator Design Pattern is a behavioral design pattern that provides a way to access elements of an aggregate object sequentially without exposing its underlying representation. It allows you to traverse the elements of a collection without exposing its internal structure, making it easier to iterate over the collection's elements.

Iterator Interface: This interface defines methods for traversing the elements of a collection, such as Next(), HasNext(), and possibly Reset().

Concrete Iterator: This class implements the iterator interface and keeps track of the current position in the collection. It provides methods to move to the next element, check if there are more elements, and retrieve the current element.

Aggregate Interface: This interface defines methods for creating an iterator object, typically named CreateIterator().

Concrete Aggregate: This class implements the aggregate interface and provides an implementation for creating an iterator object specific to its collection type.

```csharp
using System;
using System.Collections;
using System.Collections.Generic;

// Iterator interface
public interface IIterator<T>
{
    bool HasNext();
    T Next();
}

// Aggregate interface
public interface IIterableCollection<T>
{
    IIterator<T> CreateIterator();
}

// Concrete Iterator
public class ArrayIterator<T> : IIterator<T>
{
    private readonly T[] collection;
    private int index = 0;

    public ArrayIterator(T[] collection)
    {
        this.collection = collection;
    }

    public bool HasNext()
    {
        return index < collection.Length;
    }

    public T Next()
    {
        if (!HasNext())
        {
            throw new InvalidOperationException("No more elements to iterate.");
        }

        return collection[index++];
    }
}

// Concrete Aggregate
public class ArrayCollection<T> : IIterableCollection<T>
{
    private readonly T[] items;

    public ArrayCollection(T[] items)
    {
        this.items = items;
    }

    public IIterator<T> CreateIterator()
    {
        return new ArrayIterator<T>(items);
    }
}

// Client code
class Program
{
    static void Main(string[] args)
    {
        // Create an array collection
        int[] numbers = { 1, 2, 3, 4, 5 };
        ArrayCollection<int> collection = new ArrayCollection<int>(numbers);

        // Create an iterator for the collection
        IIterator<int> iterator = collection.CreateIterator();

        // Iterate over the elements
        Console.WriteLine("Iterating over the collection:");
        while (iterator.HasNext())
        {
            int element = iterator.Next();
            Console.WriteLine(element);
        }
    }
}
```
[Back](../README.md/#iterator)

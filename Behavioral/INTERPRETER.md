## The Interpreter Design Pattern

The Interpreter Design Pattern is a behavioral design pattern that is used to define a grammar for interpreting a language and to provide a way to evaluate sentences in that language. It describes how to interpret sentences in a given language and is typically used in scenarios where you need to parse and interpret expressions or statements.

Abstract Expression: This interface declares an abstract method that is common to all concrete expressions. It may also contain additional methods for setting context or interpreting the expression.

Terminal Expression: These are concrete expressions that implement the abstract expression interface and represent the terminal symbols in the grammar of the language.

Non-terminal Expression: These are concrete expressions that implement the abstract expression interface and represent the non-terminal symbols in the grammar of the language. They typically consist of combinations of terminal and non-terminal expressions.

Context: This contains information that is global to the interpreter. It may include variables or state needed for interpreting expressions.

```csharp
using System;
using System.Text.RegularExpressions;

// Abstract expression
public interface IExpression
{
    bool Interpret(string context);
}

// Terminal expression: LiteralExpression
public class LiteralExpression : IExpression
{
    private readonly string literal;

    public LiteralExpression(string literal)
    {
        this.literal = literal;
    }

    public bool Interpret(string context)
    {
        return context.Contains(literal);
    }
}

// Terminal expression: WildcardExpression
public class WildcardExpression : IExpression
{
    public bool Interpret(string context)
    {
        return true; // Wildcard matches anything
    }
}

// Non-terminal expression: OrExpression
public class OrExpression : IExpression
{
    private readonly IExpression leftExpression;
    private readonly IExpression rightExpression;

    public OrExpression(IExpression leftExpression, IExpression rightExpression)
    {
        this.leftExpression = leftExpression;
        this.rightExpression = rightExpression;
    }

    public bool Interpret(string context)
    {
        return leftExpression.Interpret(context) || rightExpression.Interpret(context);
    }
}

// Non-terminal expression: AndExpression
public class AndExpression : IExpression
{
    private readonly IExpression leftExpression;
    private readonly IExpression rightExpression;

    public AndExpression(IExpression leftExpression, IExpression rightExpression)
    {
        this.leftExpression = leftExpression;
        this.rightExpression = rightExpression;
    }

    public bool Interpret(string context)
    {
        return leftExpression.Interpret(context) && rightExpression.Interpret(context);
    }
}

// Client code
class Program
{
    static void Main(string[] args)
    {
        // Regular expression: "ab|cd"
        IExpression expression1 = new OrExpression(new LiteralExpression("ab"), new LiteralExpression("cd"));
        Console.WriteLine("\"ab|cd\" matches \"abcd\": " + expression1.Interpret("abcd"));

        // Regular expression: "a.*b"
        IExpression expression2 = new AndExpression(new LiteralExpression("a"), new AndExpression(new WildcardExpression(), new LiteralExpression("b")));
        Console.WriteLine("\"a.*b\" matches \"axyzb\": " + expression2.Interpret("axyzb"));
    }
}
```
[Back](../README.md/#interpreter)

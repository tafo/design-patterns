## The Command Design Pattern

The Command Design Pattern is a behavioral design pattern that encapsulates a request as an object, thereby allowing parameterization of clients with queues, requests, and operations. It allows you to decouple the sender of a request from the receiver by encapsulating the request as an object. This pattern enables you to parameterize objects with operations, delay the execution of a command, queue commands, and support undoable operations.

Command: This is an interface or abstract class that declares a method for executing a command.

Concrete Command: These are classes that implement the Command interface and encapsulate a specific action or request. They typically contain a reference to the receiver object and invoke a specific method on the receiver when the command is executed.

Receiver: This is the object that performs the actual work when the command is executed. It knows how to carry out the request.

Invoker: This is the object that holds the command and invokes the command when requested. It does not know how the command is carried out, but it knows how to execute it.

```csharp
using System;
using System.Collections.Generic;

// Command interface
public interface ICommand
{
    void Execute();
    void Undo();
}

// Receiver: BankAccount
public class BankAccount
{
    public string Owner { get; }
    public decimal Balance { get; private set; }

    public BankAccount(string owner, decimal initialBalance)
    {
        Owner = owner;
        Balance = initialBalance;
    }

    public void Deposit(decimal amount)
    {
        Balance += amount;
        Console.WriteLine($"{Owner} deposited {amount:C}. New balance: {Balance:C}");
    }

    public void Withdraw(decimal amount)
    {
        if (Balance >= amount)
        {
            Balance -= amount;
            Console.WriteLine($"{Owner} withdrew {amount:C}. New balance: {Balance:C}");
        }
        else
        {
            Console.WriteLine($"{Owner} cannot withdraw {amount:C}. Insufficient funds.");
        }
    }

    public void TransferTo(BankAccount recipient, decimal amount)
    {
        if (Balance >= amount)
        {
            Withdraw(amount);
            recipient.Deposit(amount);
            Console.WriteLine($"{Owner} transferred {amount:C} to {recipient.Owner}. New balance: {Balance:C}");
        }
        else
        {
            Console.WriteLine($"{Owner} cannot transfer {amount:C}. Insufficient funds.");
        }
    }
}

// Concrete Command: DepositCommand
public class DepositCommand : ICommand
{
    private readonly BankAccount account;
    private readonly decimal amount;

    public DepositCommand(BankAccount account, decimal amount)
    {
        this.account = account;
        this.amount = amount;
    }

    public void Execute()
    {
        account.Deposit(amount);
    }

    public void Undo()
    {
        account.Withdraw(amount);
    }
}

// Concrete Command: WithdrawCommand
public class WithdrawCommand : ICommand
{
    private readonly BankAccount account;
    private readonly decimal amount;

    public WithdrawCommand(BankAccount account, decimal amount)
    {
        this.account = account;
        this.amount = amount;
    }

    public void Execute()
    {
        account.Withdraw(amount);
    }

    public void Undo()
    {
        account.Deposit(amount);
    }
}

// Concrete Command: TransferCommand
public class TransferCommand : ICommand
{
    private readonly BankAccount sourceAccount;
    private readonly BankAccount destinationAccount;
    private readonly decimal amount;

    public TransferCommand(BankAccount sourceAccount, BankAccount destinationAccount, decimal amount)
    {
        this.sourceAccount = sourceAccount;
        this.destinationAccount = destinationAccount;
        this.amount = amount;
    }

    public void Execute()
    {
        sourceAccount.TransferTo(destinationAccount, amount);
    }

    public void Undo()
    {
        destinationAccount.TransferTo(sourceAccount, amount);
    }
}

// Invoker: TransactionManager
public class TransactionManager
{
    private readonly List<ICommand> transactions = new List<ICommand>();

    public void ExecuteTransaction(ICommand transaction)
    {
        transaction.Execute();
        transactions.Add(transaction);
    }

    public void UndoLastTransaction()
    {
        if (transactions.Count > 0)
        {
            ICommand lastTransaction = transactions[transactions.Count - 1];
            lastTransaction.Undo();
            transactions.RemoveAt(transactions.Count - 1);
        }
    }
}

// Client code
class Program
{
    static void Main(string[] args)
    {
        // Create bank accounts
        BankAccount aliceAccount = new BankAccount("Alice", 1000);
        BankAccount bobAccount = new BankAccount("Bob", 500);

        // Create transaction manager
        TransactionManager transactionManager = new TransactionManager();

        // Execute transactions
        ICommand depositCommand = new DepositCommand(aliceAccount, 200);
        transactionManager.ExecuteTransaction(depositCommand);

        ICommand withdrawCommand = new WithdrawCommand(aliceAccount, 300);
        transactionManager.ExecuteTransaction(withdrawCommand);

        ICommand transferCommand = new TransferCommand(aliceAccount, bobAccount, 400);
        transactionManager.ExecuteTransaction(transferCommand);

        // Undo the last transaction
        transactionManager.UndoLastTransaction();
    }
}
```
[Back](../README.md#command)

## The Memento Design Pattern

The Memento Design Pattern is a behavioral design pattern that allows you to capture and externalize an object's internal state without violating encapsulation, and later restore the object to that state. It effectively allows you to implement undo and redo functionality or save and restore mechanisms in an application.

Originator: This is the object whose state needs to be saved and restored. It creates a memento containing a snapshot of its current state and uses that memento to restore its state later.

Memento: This is an object that stores the internal state of the originator. It has two main responsibilities: storing the state of the originator and providing methods for the originator to restore its state.

CareTaker: This is an object that keeps track of mementos and provides an interface for storing and retrieving mementos. It doesn't know the internal state of the originator but manages the mementos on its behalf.

```csharp
using System;
using System.Collections.Generic;

// Memento: Represents the state to be stored
public class GameStateMemento
{
    public int PlayerHealth { get; }
    public int PlayerScore { get; }

    public GameStateMemento(int health, int score)
    {
        PlayerHealth = health;
        PlayerScore = score;
    }
}

// Originator: Object whose state needs to be saved and restored
public class Game
{
    private int _playerHealth;
    private int _playerScore;

    public Game()
    {
        _playerHealth = 100;
        _playerScore = 0;
    }

    public void Play()
    {
        // Simulate gameplay actions
        Console.WriteLine("Playing the game...");
        _playerHealth -= 10;
        _playerScore += 50;
    }

    public GameStateMemento SaveState()
    {
        return new GameStateMemento(_playerHealth, _playerScore);
    }

    public void RestoreState(GameStateMemento memento)
    {
        _playerHealth = memento.PlayerHealth;
        _playerScore = memento.PlayerScore;
        Console.WriteLine($"Game restored: Health = {_playerHealth}, Score = {_playerScore}");
    }
}

// CareTaker: Manages mementos
public class GameHistory
{
    private readonly Stack<GameStateMemento> _mementos = new Stack<GameStateMemento>();

    public void SaveState(GameStateMemento memento)
    {
        _mementos.Push(memento);
    }

    public GameStateMemento GetLastSavedState()
    {
        return _mementos.Pop();
    }
}

// Client code
class Program
{
    static void Main(string[] args)
    {
        Game game = new Game();
        GameHistory history = new GameHistory();

        // Play the game
        game.Play();

        // Save game state
        history.SaveState(game.SaveState());

        // Play some more
        game.Play();

        // Save game state again
        history.SaveState(game.SaveState());

        // Restore game state
        GameStateMemento savedState = history.GetLastSavedState();
        game.RestoreState(savedState);

        // Output: Game restored: Health = 90, Score = 50
    }
}
```
[Back](../README.md#memento)

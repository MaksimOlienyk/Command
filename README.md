# Command - Патерн Проєктування

Патерн Command інкапсулює дію у вигляді об’єкта.  
Це дозволяє передавати команди як параметри, ставити їх у черги, логувати та відміняти.

## Ідея

Замість того, щоб викликати дію безпосередньо, ми створюємо об’єкт-команду, який знає, що має виконати і над чим.  
Запит на виконання відокремлюється від його реалізації.

## Структура

| Елемент         | Опис |
|----------------|------|
| `ICommand`     | Інтерфейс команди |
| `ConcreteCommand` | Зберігає посилання на отримувача та викликає його дію |
| `Receiver`     | Об’єкт, який виконує справжню роботу |
| `Invoker`      | Клас, який викликає команду |
| Клієнт         | Створює команду та передає її виконавцю |

## Код

```csharp
interface ICommand { void Execute(); }

class Receiver {
    public void Action() => Console.WriteLine("Action performed");
}

class ConcreteCommand : ICommand {
    private Receiver _receiver;
    public ConcreteCommand(Receiver r){ _receiver = r; }
    public void Execute() => _receiver.Action();
}

class Invoker {
    private ICommand _cmd;
    public void SetCommand(ICommand c) => _cmd = c;
    public void Run() => _cmd.Execute();
}

class Program {
    static void Main() {
        var invoker = new Invoker();
        invoker.SetCommand(new ConcreteCommand(new Receiver()));
        invoker.Run();
    }
}


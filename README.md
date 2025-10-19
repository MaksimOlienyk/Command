# Command
```cs
interface ICommand { void Execute(); }

class Receiver { public void Action()=>Console.WriteLine("Action performed"); }

class ConcreteCommand : ICommand {
    private Receiver _receiver;
    public ConcreteCommand(Receiver r){_receiver=r;}
    public void Execute()=>_receiver.Action();
}

class Invoker { private ICommand _cmd; public void SetCommand(ICommand c)=>_cmd=c; public void Run()=>_cmd.Execute(); }

class Program {
    static void Main(){
        var invoker=new Invoker();
        invoker.SetCommand(new ConcreteCommand(new Receiver()));
        invoker.Run();
    }
}

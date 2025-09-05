# Interfaces, Delegates & Lambdas (Microwave Edition)

These concepts can feel tricky. Let’s break them down with something everyone knows: a **microwave**.  

---

##  Interfaces – “Microwave has rules to follow”

Think of an **interface** like a rulebook.  
If the microwave claims *“I follow these rules”*, it must provide those actions.  

```csharp
public interface IAppliance
{
    void Start();
    void Stop();
}
```

```csharp
// The Microwave follows the rules:
public class Microwave : IAppliance
{
    public void Start() => Console.WriteLine("Microwave heating food! ");
    public void Stop()  => Console.WriteLine("Microwave stopped.");
}
```

Even though the interface doesn’t know what a microwave is, it guarantees the microwave must **Start** and **Stop**.  

 Interfaces = **common rules that an object promises to follow**.

---

##  Delegates – “Control panel buttons”

A **delegate** is like the **buttons on the microwave** .  
You don’t care how it heats the food — you just press the button.  

```csharp
delegate void ButtonAction();

class ControlPanel
{
    public void Press(ButtonAction action)
    {
        action(); // run whatever method is stored
    }
}
```

```csharp
// Usage:
var panel = new ControlPanel();
var microwave = new Microwave();

panel.Press(microwave.Start); // Microwave heating food! 
panel.Press(microwave.Stop);  // Microwave stopped.
```
 The same button (`ButtonAction`) can point to different methods, just like microwave buttons can trigger different actions.

---

##  Lambdas – “Quick one-off buttons”

Sometimes you want a **custom button** without creating a whole new method.  
That’s where **lambdas** come in:  

```csharp
var panel = new ControlPanel();

panel.Press(() => Console.WriteLine("Beep! Timer finished "));
panel.Press(() => Console.WriteLine("Door opened "));
```
 Lambdas are like **sticky-note buttons** you add on the fly.

---

##  Quick Recap

- **Interfaces** → define the rules (Microwave = Start & Stop).  
- **Delegates** → act like control panel buttons that trigger actions.  
- **Lambdas** → quick, throwaway buttons you can create on the spot.  

 These tools make your code **flexible**, **reusable**, and **easy to extend**.  

---

##  Challenge for You

1. Add a new action `Pause()` inside the microwave.  
2. Create a delegate called `CustomAction` for secret microwave tricks.  
3. Use a lambda to make your microwave say:  

```csharp
() => Console.WriteLine("Microwave says: Enjoy your meal! ")
```

---

*Now you’re ready to tackle Week 8 with a clearer picture — microwaves only!* 

---

##  Challenge Solution

Here’s one way to solve the challenge step by step:

```csharp
using System;

public interface IAppliance
{
    void Start();
    void Stop();
}

public class Microwave : IAppliance
{
    public void Start() => Console.WriteLine("Microwave heating food! ");
    public void Stop()  => Console.WriteLine("Microwave stopped.");
    
    // New action Pause()
    public void Pause() => Console.WriteLine("Microwave paused");
}

// Delegate for secret microwave tricks
delegate void CustomAction();

class Program
{
    static void Main()
    {
        var microwave = new Microwave();

        // Normal actions
        microwave.Start();
        microwave.Pause();
        microwave.Stop();

        //  Use a lambda with delegate
        CustomAction secret = () => Console.WriteLine("Microwave says: Enjoy your meal! ");
        secret(); // run the secret trick
    }
}
```

###  What’s Happening Here?
1. **Pause method** is added directly to `Microwave` class so now it has `Start()`, `Stop()`, and `Pause()`.  
2. **Delegate `CustomAction`** now works like a “secret button” you can assign to any special trick.  
3. **Lambda expression**, quickly prints `"Microwave says: Enjoy your meal! "` without needing a full method.  

---



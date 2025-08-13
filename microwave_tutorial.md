# Building a Microwave Simulator with SplashKit

## Introduction
In this tutorial, we will build a simple **Microwave Simulator** using [SplashKit](https://www.splashkit.io/).  
The simulator will display:
- A microwave with a door and keypad
- Start and Stop buttons
- Controls using keyboard keys

By the end you will know how to make shapes put in text and handle controls in SplashKit using C# while also using encapsulation which is a main idea in OOP
---

## Understanding Encapsulation
Before we start coding, let’s quickly go over **encapsulation**.  
Encapsulation means bundling data (fields) and the actions that operate on that data (methods) into a single unit (class), while controlling how outside code can interact with it.

I made a short video that explains encapsulation with a **microwave metaphor** - perfect for this project:  
[![Encapsulation Explained - Microwave Metaphor](https://img.youtube.com/vi/oHY06wmhwoc/0.jpg)](https://youtu.be/oHY06wmhwoc)

---

## Project Setup
1. Open your terminal (**MSYS2 MinGW64** if using the Deakin SplashKit setup) and create a new project folder:
   ```bash
   mkdir MicrowaveSplashkit
   cd MicrowaveSplashkit
   ```
2. Create a new SplashKit C# console project:
   ```bash
   skm dotnet new console
   ```
3. Restore dependencies:
   ```bash
   skm dotnet restore
   ```
4. Run the file:
    ```bash
    code .
    ```
5. You will have the `Program.cs` but you should create `Microwave.cs` as well

6. Run the program when we finish the code with  the below line:
   ```bash
   skm dotnet run
   ```

---

## File 1: `Microwave.cs`

This file defines our **Microwave** class.  
It is responsible for:
- Storing the microwave’s **state** (door open/closed, cooking/idle)
- Providing **methods** to change the state
- Drawing the microwave graphics on the screen

```csharp
using SplashKitSDK;
using System;

public class Microwave
{
    private bool _doorOpen = false; // Is the door open?
    private bool _isCooking = false; // Is the microwave cooking?

    // Opens the door
    public void OpenDoor() => _doorOpen = true;

    // Closes the door
    public void CloseDoor() => _doorOpen = false;

    // Starts cooking only if the door is closed
    public void StartCooking()
    {
        if (!_doorOpen) _isCooking = true;
    }

    // Stops cooking
    public void StopCooking() => _isCooking = false;

    // Draws the microwave on screen
    public void Draw(float x, float y)
    {
        // Microwave body
        SplashKit.FillRectangle(Color.Gray, x, y, 300, 200);

        // Door
        SplashKit.FillRectangle(Color.Black, x + 10, y + 10, 120, 180);
        if (_doorOpen)
            SplashKit.DrawText("Door Open", Color.White, x + 25, y + 90);

        // Control panel
        float panelX = x + 150;
        SplashKit.FillRectangle(Color.Black, panelX, y + 10, 140, 180);

        // Keypad
        float keyW = 40, keyH = 30, gap = 5;
        for (int row = 0; row < 3; row++)
        {
            for (int col = 0; col < 3; col++)
            {
                SplashKit.FillRectangle(Color.Gray,
                    panelX + col * (keyW + gap),
                    y + 40 + row * (keyH + gap),
                    keyW, keyH);
            }
        }

        // Start/Stop buttons
        float btnGap = 6;
        float btnW = (keyW - btnGap) / 2;
        float btnH = 24;
        float btnY = y + 140;
        float startX = panelX;
        float stopX = startX + btnW + btnGap;

        // Start button (red)
        SplashKit.FillRectangle(Color.RGBColor(180, 40, 40), startX, btnY, btnW, btnH);
        SplashKit.DrawText("Start", Color.White, startX + 4, btnY + 4);

        // Stop button (green)
        SplashKit.FillRectangle(Color.RGBColor(40, 150, 60), stopX, btnY, btnW, btnH);
        SplashKit.DrawText("Stop", Color.White, stopX + 4, btnY + 4);

        // Status text
        string status = _isCooking ? "Cooking..." : "Idle";
        SplashKit.DrawText(status, Color.White, panelX + 40, y + 20);
    }
}
```

---

## File 2: `Program.cs`

This is our **entry point**.  
It:
- Creates the game window
- Instantiates the microwave
- Listens for **keyboard input**
- Calls the `Draw()` method to display the microwave

```csharp
using SplashKitSDK;

public class Program
{
    public static void Main()
    {
        // Create a window for the simulator
        Window window = new Window("Microwave Simulator", 500, 300);

        // Create a Microwave object
        Microwave microwave = new Microwave();

        // Main game loop
        while (!window.CloseRequested)
        {
            SplashKit.ProcessEvents(); // Handle input/events
            SplashKit.ClearScreen(Color.Teal); // Clear screen before drawing

            // Keyboard controls
            if (SplashKit.KeyTyped(KeyCode.OKey)) microwave.OpenDoor();
            if (SplashKit.KeyTyped(KeyCode.CKey)) microwave.CloseDoor();
            if (SplashKit.KeyTyped(KeyCode.SKey)) microwave.StartCooking();
            if (SplashKit.KeyTyped(KeyCode.SpaceKey)) microwave.StopCooking();

            // Draw the microwave
            microwave.Draw(100, 50);

            SplashKit.RefreshScreen(); // Update the display
        }
    }
}
```

---

## Controls
- **O** – Open door  
- **C** – Close door  
- **S** – Start cooking (only if door is closed)  
- **Space** – Stop cooking  

---

## Wrap-Up
You have now built a **Microwave Simulator** using SplashKit and applied **encapsulation** by keeping all microwave-related data and functions inside the `Microwave` class.

Possible extensions:
- Add a countdown timer
- Play a “ding” sound when cooking finishes
- Replace rectangles with actual images

---

##  Output Demo Video
Watch the final output of our Microwave Simulator here:  

[![Microwave Simulator Output](https://img.youtube.com/vi/DxEg7KDytdg/0.jpg)](https://youtu.be/DxEg7KDytdg?si=fKvi8gUARXC812WR)

---

**Happy coding with SplashKit!**

# Global-Low-Level-Key-Board-And-Mouse-Hook
A simple description and sample of creating a global low level keyboard And Mouse hook in C#

# Introduction
Keyboard MouseHooks C# Library is part of for .NET developers. It enables you via C# events system to install and track low level Windows keyboard and Mouse hooks.

# Background
I've found a lot of hook and simulator code out there, but a lot of it was not very organized, and a bit hard to use. The goal here is to make a very simple and easy-to-use library for mouse and keyboard operations not natively supported by .NET.

# Installing Global Keyboard and Mouse Hooks
This section will explain how to use the global KeyboardHook and MouseHook hooks which can capture mouse and keyboard events from any application. These events are very similar to the ones that appear on Windows controls, so they should look familiar.

Using the Mouse Hook:

```
// Create the Mouse Hook

MouseHook mouseHook = new MouseHook();

// Create the Keyboard Hook
KeyboardHook keyboardHook = new KeyboardHook();

 // Capture the events
 mouseHook.MouseMove += new MouseHook.MouseHookCallback(mouseHook_MouseMove);


 //Installing the Mouse Hooks
 mouseHook.Install();
Using the Keyboard Hook:

 // Capture the events
 keyboardHook.KeyDown += new KeyboardHook.KeyboardHookCallback(keyboardHook_KeyDown);
 keyboardHook.KeyUp += new KeyboardHook.KeyboardHookCallback(keyboardHook_KeyUp);

 //Installing the Keyboard Hooks
 keyboardHook.Install();
```

```keyboardHook.KeyDown +=```

...and then hit TAB two times. Visual Studio will finish the rest of the line, and will go out and create the blank method for you. This is a nice feature, and saves a lot of time; use it!

```
private void keyboardHook_KeyUp(KeyboardHook.VKeys key)
{
 Console.WriteLine("[" + DateTime.Now.ToLongTimeString() + "] KeyUp Event {" + key.ToString() + "}");
} 
private void keyboardHook_KeyDown(KeyboardHook.VKeys key) 
{ 
 Console.WriteLine("[" + DateTime.Now.ToLongTimeString() + "] KeyDown Event {" + key.ToString() + "}" ); 
}
```

# Uninstalling Global Keyboard and Mouse Hooks
For uninstalling the Global hook, this can be done on the AplicationExit event. For getting the Application Exit event, we have to Register Application exit event on the Form Load.

```
// Handle the ApplicationExit event to know when the application is exiting.
   Application.ApplicationExit += new EventHandler(this.OnApplicationExit); 
```

```
private void OnApplicationExit(object sender, EventArgs e) 
{
 keyboardHook.KeyDown -= new KeyboardHook.KeyboardHookCallback(keyboardHook_KeyDown);
 keyboardHook.KeyUp -= new KeyboardHook.KeyboardHookCallback(keyboardHook_KeyUp);
 keyboardHook.Uninstall();
 mouseHook.MouseMove -= new MouseHook.MouseHookCallback(mouseHook_MouseMove);
  mouseHook.Uninstall();
 }
 ```

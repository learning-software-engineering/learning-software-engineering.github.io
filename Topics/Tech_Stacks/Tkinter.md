# Tkinter

## Introduction

Tkinter is a Python GUI framework that comes with the Python standard library, Tkinter is cross-platform and the visual elements are rendered using native operating system elements.

Tkinter is considered the go-to Python GUI framework, but GUIs built with Tkinter are often considered aesthetically unpleasing with designs often considered outdated. Given this, Tkinter is recommended for proprietary business side applications.

Tkinter is lightweight and easy to learn compared to other GUI frameworks. This makes it a valid candidate when selecting a framework for GUI applications in Python. Especially if the priority is to quickly build a functional application.

In this introduction, we will be building a basic GUI and familiarising ourselves with some Tkinter components.

---
### Prerequisites:
- Basic knowledge of Python
- Python installed on your system


## Core Components

A Tkinter GUI has two main components

1. **The base GUI window:** Windows are the main container in which all of the other GUI elements sit inside. These other elements are known as widgets, widgets can come in many forms.

2. **Widgets:** All GUI elements that are inside a window, these can come in many forms, such as buttons, textboxes or labels.
 


## Setting Up

Lets begin by creating a new Python file and importing Tkinter

```python
import tkinter as tk
```
   
And that's all there is to it, you have successfully set up Tkinter.

### Creating a window
Here is a simple example of creating a default Tkinter window, add these two lines of code to your file:
```python
import tkinter as tk
window = tk.Tk()
window.mainloop()
```

When you run the file, you should see the blank window open up. This is the blank Tkinter window

The first line initialises a Tkinter window while the second line runs its "main loop" or the loop that displays the window and waits for events.

### Adding widgets

#### Labels
Lets add a simple textbox to the window that says "Hello world".

Between our current two lines of code, add the following two lines

```python
greeting = tk.Label(window, text="Hello world")
greeting.pack()
```

the resulting file should now look like:

```python
import tkinter as tk

window = tk.Tk()

greeting = tk.Label(window, text="Hello world")
greeting.pack()

window.mainloop()
```
`greeting = tk.Label(window, text="Hello world")` creates a Label widget and makes it a child element of `window`

`greeting.pack()` is a rough way to tell the window to show the widget `greeting` in the window, there are other methods to display elements with more precision such as `grid()` which determines a grid location for the element relative to other elements in the same window.

Notice that `window.mainloop()` needs to be run last to process any updates you made to window

#### Buttons

Buttons are one of the most basic ways to implement Python logic into your GUIs

Lets create a basic counter that instead of displaying Hello world, it prints it to standard out, first lets define a printer function that prints what we want

```python
def greeter():
    print("Hello world")
```

now to create the button we create and pack it similarily like the Labels from earlier

```python
button = tk.Button(window, text="greet!", command = greeter)
button.pack()
```

Notice however, that the Button accepts the parameter `command` which is the function name we want to call when the button is pressed

Putting it together, the Python file should look something like this:

```python
import tkinter as tk

def greeter():
    print("Hello world")

window = tk.Tk()

button = tk.Button(window, text="greet!", command = greeter)
button.pack()

window.mainloop()
```
The resulting GUI that appears when you run the program should display a button labeled "greet!" that prints "Hello world" when clicked to standard out

## Conclusions
Tkinter is a very lightweight, easy to learn and powerful GUI that is suitable for quickly building and implementing business side logic and monitoring. While its visual design is unsuitable for client side applications, it still a useful library to pick up as it is an ubiqitous framework present in all installations of Python.


## Useful Links
- [Tkinter documentation](https://docs.python.org/3/library/tkinter.html)
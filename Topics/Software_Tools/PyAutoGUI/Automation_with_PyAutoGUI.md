# PyAutoGui Tutorial: Automate Tasks with Python

PyAutoGui is a Python module that allows you to programmatically control the mouse and keyboard to automate tasks. In this tutorial, we'll cover the basics of PyAutoGui and some advanced features. You can find the official documentation for it [here](https://pyautogui.readthedocs.io/en/latest/index.html).

## Requirements
- PyAutoGUI works on Windows/Mac/Linux and on Python 2 & 3.
- So you will need to have installed Python first. You can refer to [this website](https://realpython.com/installing-python/) for installation details.
- This tutorial shows examples in Python 3.

## What can you do with PyAutoGUI?
- **Simulate mouse movement:** The mouse can be moved to any desired location on the screen and used to click on things as well.  
  *You can*: Automate the process of clicking through a series of buttons in a software application.

- **Simulate keypresses:** Simulate keypresses without having to touch the keyboard.  
  *You can*: Automate the process of filling out a form on a website by simulating keypresses to enter text.

- **Take screenshots.**  
  *You can*: Capture screenshots of the entire screen or just a portion of it to document the state of a program or website.

- **Find a particular image on a screen.**  
  *You can*: Locate a specific image within the current screen to automate tasks that require interacting with elements that are not easily accessible through other means.

- **Display alerts and message boxes.**  
  *You can*: Provide feedback to the user or prompt the user to take a specific action by displaying custom alerts and message boxes on the screen.


## Installation

To use PyAutoGui, you need to install it first. You can install it using pip:

```bash
pip install pyautogui
```

## Getting Started
Create a brand new python file and import pyautogui

```python
import pyautogui
```

## Positions on the Screen
Before we start moving the mouse around, we must first understand how points on your screen are defined and used by PyAutoGUI. Locations on your screen are defined using $x$ and $y$ coordinates. But unlike in your math courses, the origin, or (0, 0), is located at the top left, instead of the bottom left. 

For example, if you have a 500x500p display, here is how pixels/locations are mapped on your screen.

![pixel-coordinates](./assets/screenCoord.png)
(from Coordinates and Modes - CMPT 166 Fall 2016 1 documentation. (n.d.). https://www2.cs.sfu.ca/CourseCentral/166/tjd/coordinates.html)

You can use PyAutoGUI to get your screen resolution size like this:
```python
>>> pyautogui.size()
Size(width=2304, height=1296) # weird mac displays
```

## Mouse Control

### Mouse Movements
Now you're ready to move your mouse around! 
To do so, PyAutoGUI provides us with `moveTo()` and `move()`

`moveTo()` allows you to move the mouse to a specific location on the screen.
```python
>>> pyautogui.moveTo(100, 200)   # moves mouse to X of 100, Y of 200.

>>> pyautogui.moveTo(None, 500)  # wont change the X coordinate of the mouse, just the Y. 
# So the mouse moves to X of 100, Y of 500

>>> pyautogui.moveTo(600, None)  # Similarly, moves mouse to X of 600, Y of 500.
```

`move()` on the other hand lets you move the mouse to a location relative to its current one.
```python
>>> pyautogui.move(10, 0) # move the mouse 10 pixels to the right
>>> pyautogui.move(-50, 100) # move the mouse 50 pixels to the right and 100 pixels up
```

This movement is instantaneous, but both these functions also take a third argument, which can be used to change the duration of the movement in seconds.

```python
>>> pyautogui.move(10, 0, 2) # move the mouse 10 pixels to the right over 2 seconds
>>> pyautogui.moveTo(100, 200, 10)   # moves mouse to X of 100, Y of 200 over 10 seconds
```

How do I know where to move my mouse? Well here is a simple trick that you can use to find the $(x, y)$ coordinates of a pixel on your screen:

```python
import pyautogui
import time

time.sleep(5) # 5 second buffer to let you move your mouse
print(pyautogui.position()) # prints the current position of the mouse
```
All you have to do is simply run the program above and move your mouse to the location you want the coordinates for (make sure its within 5 seconds). The output will tell you exactly where the mouse is!

### Clicking
Now that you can move your mouse around freely to wherever you want, how do you finally perform a mouseclick? PyAutoGUI provides multiple options as follows:
```python
>>> pyautogui.click()  # perform a simple left-click
>>> pyautogui.click(x=450, y=230)  # move to 450, 230, then left-click
>>> pyautogui.click(button='right')  # right-click the mouse
>>> pyautogui.doubleClick()  # double left-click
>>> pyautogui.click(clicks=3)  # triple left-click
>>> pyautogui.click(button='right', clicks=4, interval=0.5) #quadruple right-click 
# but with a 0.5 second pause in between the clicks
```

### Other Cool Mouse Functions
There's a lot more than just clicking that you can do with the PyAutoGUI mouse.
Here are a few examples:
```python
>>> pyautogui.dragTo(300, 400, 2, button='left')  # drag mouse to X of 300, Y of 400 over 2 seconds while holding down left mouse button
>>> pyautogui.drag(30, 0, 2, button='right')   # drag the mouse left 30 pixels over 2 seconds while holding down the right mouse button
>>> pyautogui.scroll(10)   # scroll up 10 "clicks"
>>> pyautogui.hscroll(-10)  # scroll left 10 "clicks"
```
Go check out the [docs](https://pyautogui.readthedocs.io/en/latest/mouse.html) for a lot more!

## Locating Images and Screenshots
Let's say you want to click on something that's going to pop up on the screen but you don't know where it's going to be. PyAutoGUI has just the solution for that. 

Suppose you want to open the UofT folder on your desktop below, but you don't want to bother finding its coordinates.
![desktop](./assets/desktop.png)

First take a screenshot of the folder and save it:

![desktop](./assets/uoft_folder.png)

You have two options:
- Locate the center of the folder and click on it
```python
>>> import pyautogui
>>> uoft_folder = pyautogui.locateOnScreen('uoft_folder.png')
>>> uoft_mid = pyautogui.center(uoft_folder)
>>> uoft_midx, uoft_midy = uoft_mid
>>> pyautogui.click(uoft_midx, uoft_midy, clicks=2)
```

- Or you could take advantage of the PyAutoGUI shorthands
```python
>>> import pyautogui
>>> pyautogui.click('uoft_folder.png') # yes it's that easy
```

Additionally, PyAutoGUI also provides screenshot functionality, in case you need it.
```python
>>> import pyautogui
# Takes a screenshot and returns an PIL Image object
>>> im1 = pyautogui.screenshot()
# This one also saves the screenshot with the name being the string passed in
>>> im2 = pyautogui.screenshot('my_screenshot.png')
# You can also take screenshots of specific regions by specifying the x,y coordinates of the top left and bottom right of the desired region
>>> im3 = pyautogui.screenshot(region=(0,0, 300, 400))
```

### Putting it together
Here is an example of how you can locate the UofT folder, drag it 400 pixels to the left, and then open it.
```python
import pyautogui
uoft_folder = pyautogui.locateOnScreen('uoft_folder.png')
uoft_midx, uoft_midy = pyautogui.center(uoft_folder)
pyautogui.moveTo(uoft_midx, uoft_midy, 1)
pyautogui.drag(-400, 0, 1, button='left')
pyautogui.doubleClick()
```
![sample_gif](./assets/move_folder.gif)


## Keyboard Controls
Once familiar with mouse functions, exploring keyboard interactions becomes the next vital step. PyAutoGui offers various methods for keyboard input, enhancing automation capabilities.

Some use cases where keyboard functionality in software engineering can be highly beneficial are:
- **Simulating user input:** Using keyboard functions like `write()` and `press()` allows developers to simulate user input, filling out forms with predefined data efficiently.
- **Keyboard Shortcuts for Navigation:** Many software applications rely on keyboard shortcuts for quick navigation and task execution. Implementing keyboard shortcuts using PyAutoGui's `hotkey()` function can enhance user productivity and streamline workflow in software development environments.
- **Integration Testing:**  During integration testing, developers often need to simulate complex user interactions, including keyboard inputs. PyAutoGui's keyboard functions enable developers to programmatically trigger key presses, facilitating thorough testing of software systems under various scenarios.
- **Command-Line Interfaces (CLI):** Many software tools and utilities feature command-line interfaces (CLI) for interaction. PyAutoGui's keyboard functions can be utilized to automate CLI interactions, allowing developers to script and execute repetitive tasks with ease.

We can write something using the `write()` keyword. This will simply type the argument that is passed into it, which is a string.

```python
>>> pyautogui.write('Engineering!\n')                  # Prints 'Engineering'
>>> pyautogui.write('Engineering!', interval=0.25)   # Similar to the move function, the second argument is
                                                     # the interval between pressing each button
```
As an example, the above function gives the following output:

<img width="297" alt="Screenshot 2024-03-17 at 10 03 12 PM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/97929147/e106b3d7-33e7-40ff-81c7-5e248941c63f">

However, one may wonder what may happen if we inturrupt the program mid execution. For instance the following happens when we click the caps lock button while executing the above program with interval after printing the first 6 characters.

<img width="430" alt="Screenshot 2024-03-17 at 10 06 03 PM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/97929147/b3c44659-fb55-4afa-bec8-c7adaba542b0">

The keyboard just switched to caps lock after the point it was pressed.

We may sometimes want to just click on a button on the keyboard, which is not a string, like the enter or the shift button. For this, we can use the `press()` function.

```python
>>> pyautogui('shift')    # Presses the shift button
```
We can similarly use a range of buttons. For the full list, please see the documentation.

Sometimes we may want to press more than one button at a time. For this we can use the `keyUp()` and the `keyDown()` function as done in the following:
```python
>>> pyautogui.keyDown('ctrl')    # Press the ctrl button down
>>> pyautogui.press('p')         # Press the 'p' button and release it
>>> pyautogui.keyUp('ctrl')      # Lift the press from the ctrl button
```

To press multiple keys sequentially, pass a list of strings to `press()`:

```python
>>> pyautogui.press(['tab', 'tab', 'tab'])   # Presses 'tab' key thrice
>>> pyautogui.press('tab', presses=3)        # Sets the number of presses
```

The `hold()` Context Manager: For holding a key conveniently within a context block, `hold()` function serves as a useful tool:

```python
>>> with pyautogui.hold('ctrl'):
        pyautogui.press(['tab', 'tab', 'tab'])
```

The `hotkey()` Function: To execute hotkeys or keyboard shortcuts efficiently, utilize the `hotkey()` function:

```python
>>> pyautogui.hotkey('ctrl', 'shift', 'p')   # Executes Ctrl + Shift + p
```
These functionalities empower users with versatile keyboard interactions, facilitating seamless automation tasks.



## Message Box Functions
PyAutoGui leverages PyMsgBox's message box functions, offering a cross-platform, pure Python solution for displaying JavaScript-style message boxes. These functions serve various purposes and provide flexibility in handling user interactions seamlessly. Here's an overview of the four message box functions provided:

### The alert Function

Displays a simple message box with customizable text and a single OK button. It returns the text of the button clicked on by the user.

```python
pyautogui.alert(text='Text', title='Title', button='Button')
```
Output:

<img width="391" alt="Screenshot 2024-03-17 at 10 15 58 PM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/97929147/75f86180-6a88-46ef-8fa3-2ad092f941e6">

The meaning of the arguments can be clearly understood when looking at the output.

### The confirm Function

Displays a message box with configurable text and buttons, typically OK and Cancel. Users can choose between the provided options, and it returns the text of the button clicked.

```python
pyautogui.confirm(text='Text', title='Title', buttons=['OK', 'Cancel'])
```
Output:

<img width="390" alt="Screenshot 2024-03-17 at 10 17 55 PM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/97929147/cdece517-c1dc-4725-aed0-545bc489b3b5">


### The prompt Function

Shows a message box with text input field, along with OK and Cancel buttons. Users can input text, and it returns the entered text or None if Cancel was clicked.

```python
pyautogui.prompt(text='Text', title='Title', default='Default')
```
Output:

<img width="345" alt="Screenshot 2024-03-17 at 10 18 46 PM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/97929147/14a6869b-1abb-4b43-a530-ffe1d4b0e479">

### The password Function

Similar to the `prompt()` function, it displays a message box with a text input field. However, the typed characters are masked, typically with asterisks (*). It returns the entered text or None if Cancel was clicked.

```python
pyautogui.password(text='', title='', default='', mask='*')
```
Output:

<img width="342" alt="Screenshot 2024-03-17 at 10 19 35 PM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/97929147/ac238e45-de2e-4dd9-b64b-99c90e77eccd">


These functions empower users to handle various types of user interactions effectively within their Python scripts, enhancing the user experience and interactivity of their applications.

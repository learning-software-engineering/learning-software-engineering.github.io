## Debugging in Python

One of the most important skills to have as a software developer is how to debug. Although it can be tempting to simply use print statements everywhere to debug, this method quickly gets messy as the code base grows. Luckily, python has a module called pdb which makes debugging much easier to manage! 


Pdb is an interactive source code debugger for Python programs. This tool allows programmers to step through each line of code individually and inspect the values of all the variables. The commands will be discussed in more detail below. 

Firstly, to get started, you must import pdb into your program, using:

```import pdb ```

Then, insert the following line of code at the location where you want the debugger to stop and allow you to step through the code.

```breakpoint()```

This will allow the debugger to run the program normally up to this line. 


##PDB Commands 

The table below shows some of the most commonly used or important commands in pdb. Many of the commands can be abbreviated, as shown below. 

| Command   | Abbreviations  | Description                                                                                                                                                                                                                                             |
|-----------|----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| help      | h              | This command can be used if you’re stuck on how to use pdb. If no arguments are given, it will print out the list of commands that pdb recognises. If a command is given as an argument, then it will print instructions about how to use that command. |
| args      | a              | Prints the list of arguments of the current function                                                                                                                                                                                                    |
| continue  | c / cont       | Runs the code up to the next breakpoint, or the end of the program if there are no other breakpoints                                                                                                                                                    |
| list      | l              | Prints the 11 lines of source code around the current line.                                                                                                                                                                                             |
| long list | ll             | Without any arguments, list all source code for the current function or frame. If one argument is given, print 11 lines around that line. If two arguments are given, list the given range. The current line in the current frame is indicated by ->    |
| next      | n              | Continue executing until the next line is reached, or the function returns                                                                                                                                                                              |
| return    | r              | Continue execution until the current function returns                                                                                                                                                                                                   |
| step      | s              | Executes the current line, stopping at the first possible occasion (either in a function that is called or on the next line in the current function                                                                                                     |
| quit      | q              | Exit the debugger                                                                                                                                                                                                                                       |



If you enter a blank line, the previous command will be repeated. The only exception to this is when the last command was list. In this case, the next 11 lines will be printed, instead of the same 11 lines. 

If you would like to read more about the further uses of the debugger, you can reference the pdb docs here: https://docs.python.org/3/library/pdb.html 

## Using Print Statements to Debug:

It can be tempting to simply use print statements everywhere to see the immediate values of the variables in the program. It is definitely quick and an intuitive way to debug. However, as your programs increase in length, the code can get very messy very quickly. Having too many print statements can become very difficult to manage. Sometimes, it’s even easy to forget what a print statement was referring to. For these reasons, it is bad practice to use print statements to debug, and tools like pdb should be utilized instead. 

Python also offers other tools to aid with debugging, but these are not inbuilt into Python, unlike pdb. Some of these tools are listed below. 

Pycharm 
- Pycharm is an IDE that is commonly used to write python scripts
- It allows you to add a breakpoint using it’s interface, but adding a red dot on one the lines
- Then, a console will pop up where you can step through each individual line of code 
- Using PyCharm instead of pdb may be useful if you prefer to use a interactive console, rather than typing out typing out commands
- Read about how to use the pycharm debugger here: https://www.jetbrains.com/help/pycharm/debugging-your-first-python-application.html#where-is-the-problem 

Sentry 
- This is a third party error-tracking and performance monitoring tool
- Specializes in monitoring web applications, which are often written in python 
- Sentry is useful for monitoring live applications, but can be paid after a certain level of usage.
- https://sentry.io/for/python/ 
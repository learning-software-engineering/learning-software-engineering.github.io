# Introduction to ```make``` and Makefiles

## Table of contents

### [Introduction](#introduction-1)

### [Basic Makefile Characteristics](#basic-makefile-characteristics-1)

### [Making a Makefile](#making-a-makefile-1)

### [Managing Multiple Directories with Makefiles](#managing-multiple-directories-with-makefiles-1)

### [Advantages and Disadvantages to ```make``` and Makefiles](#advantages-and-disadvantages-to-make-and-makefiles-1)

### [Additional Resources](#additional-resources-1)

### [Footnotes](#footnotes-1)

## Introduction

#### What are ```make``` and Makefiles
```make``` is a software build automation tool that builds programs and libraries, and determines what needs to be recompiled. It accomplishes this by using Makefiles that specify compilation targets and link their dependencies, and checking their last modified dates during compilation. This guide will cover the basics of GNU make, some example usage, and some of the advantages and disadvantages of ```make``` and Makefiles. Hopefully, by the end of this guide you will be able to decide if ```make``` is right for you.

## Basic Makefile Characteristics

#### Target

A target is the name of a task to be executed. It is typically the name of some executable or object files to be generated. A phony target is a target not named after a file.

#### Prerequisite

Prerequisites are files or tasks that the target depends on as inputs to create the target. If prerequisites have been changed since the last build, the target will be considered outdated and will need to be rebuilt.

#### Recipe

A recipe is an action that ```make``` will execute for the target it is under. It can be one or more commands, but each single recipe line must be preceded by a tab character<sup><a href=#1>1</a>.</sup>

#### Rule

Rules put the above together and link together the prerequisites to the target and define the recipes ```make``` will carry out for the designated target. By default, the first target of the first rule in the Makefile will be run by ```make```, other rules would have to be explicitly referenced by ```make target-name```.  

Rules are typically defined in this template below:
<pre>
<i>target ...</i> : <i>prerequisites...</i>
      <i>recipe</i>
      <i>...</i>
</pre>

#### Variables

Variables store values to be used throughout the file that will be substituted in whenever the variable is referenced.  

Basic variables are defined and referenced in the manner below:
<pre>
<i>variable</i> = <i>text</i> ...
$(<i>variable</i>)
</pre>

#### Functions

Functions can be called to process some argument(s) and substitute some text similar to a variable. These functions are predefined by ```make```.

Functions are typically called in the manner below:
<pre>
$(<i>functionname param,param,...</i>)
</pre>

## Making a Makefile

#### Running a Simple Makefile

The following will be written in a file called "Makefile", because make will automatically look for a file of that name in the current directory<sup><a href=#2>2</a>.</sup>.  
For the following example, we will consider a simple C program with the source code files ```main.c``` and ```helper.c``` that will be compiled into the file ```program```:

```
# Compiler and compiler flags
CC = gcc

# Rule to build the executable
program: main.o helper.o
	$(CC) -o program main.o helper.o

# Rules to build the object files
main.o: main.c
	$(CC) -c main.c

helper.o: helper.c
	$(CC) -c helper.c
```

This example first defines the variable CC to refer to the gcc compiler. Then it writes the rules to build the executable and its prerequisites. If we run we will get the following:

```bash
$ make
>>> gcc -c main.c
>>> gcc -c helper.c
>>> gcc -o program main.o helper.o
```

Then, when the rule for the target ```program``` is run by default, it will check the prerequisites ```main.o``` and ```helper.o``` and run the rules for those two targets, executing the respective gcc compilation recipes. Once it has completed the prerequisites, it will execute its own gcc compile command. The result is that ```program```, ```main.o```, and ```helper.o``` will be created in the same directory. When the target is a file, like the first three rules above, it will recompile if any of the prerequisites change, i.e. ```main.o``` will recompile if ```main.c``` has changed since the last compilation.  
Then if we run the same command again without changing any of the files, we would get the output:

```bash
$ make
>>> make: 'program' is up to date.
```

This is because none of the dependent prerequisites have been changed, so the program file is up to date. The same will occur if we explicitly call any of the other program targets (e.g. ```make main.o```). But if we want the program to be compiled on every ```make``` call, we should use phony targets.

#### Phony Targets

Phony targets are useful because unlike file targets, their rule will run every time the target comes up for remaking. A common example of this is the ```clean``` target, that is usually used to clean up the directory or library to remove the generated build artifacts. Below is an example of clean that removes all the .o object files in the directory:

```
clean:
	rm *.o
```

But for a phony target like this, if a file with the name corresponding to the target is ever created in this directory, the target would no longer be a phony target. ```make``` would check the ```clean``` file and would deem that it is up to date, and would not run its recipe. Therefore an explicit declaration that a target is phony can be made, using the special target ```.PHONY```. It would be added to the above example like so:

```
.PHONY: clean
clean:
	rm *.o
```

#### Variable Assignment

In the above example Makefile, the gcc variable was set with ```CC = gcc```. This is a recursively expanded variable. This would simply evaluate to ```gcc``` when referenced. But if it were to reference another variable, it would expand upon the referenced variable. For example if it were to be written like this:
```
GCC = cc
CC = $(GCC)
GCC = gcc
```

Then ```$(CC)``` would evaluate to ```gcc```, as it references the ```GCC``` variable, which is redefined to ```gcc```. To avoid this behaviour, which can also end up being slow with more layers, as well as self-reference issues like ``CC = $(CC) -o```, which causes an infinite loop error, simply expanded variables can be used.  
Simply expanded variables will simply expand any references during assignment and store the value, rather than the reference, aka it stores the values at the time the variable was defined. Simply expanded variables are defined in the following manner:

<pre>
<i>VARIABLENAME</i> := <i>value, ...</i>
</pre>

Doing the same variable assignments above with simply expanded variables:
```
GCC := cc
CC := $(GCC)
GCC := gcc
```

Then, ```CC``` would evaluate to ``cc``, as determined at the time of assignment.  
This behaviour makes recursively expanded variables usually more suited for static variables, while simply expanded variables are usually more suited for dynamic variables.  

Additionally, to append to a variable, use ```+=```. For the following example, ```CC``` would evaluate to ```gcc -o```: 

```
CC := gcc
CC += -o
```

#### Automatic Variables

When you cannot manually reference a target or prerequisite, you can use automatic variables that are computed for each executed rule. These are some simple useful ones:
- ```$@```: The target name
- ```$<```: The first prerequisite's name
- ```$^```: All prerequisite names
- ```$?```: All prerequisite names newer than the target

#### Pattern Rules:

Instead of manually writing a target for each object file like in the previous simple Makefile, pattern rules can be used. They are used as a list of targets that the rule will apply to, along with a target pattern that extracts the stem out of the target name, and uses it to match to the prerequisite pattern. They are written in the following template:

<pre>
<i>targets ...</i> <i>target-pattern</i>: <i>prerequisite-patterns ...</i>
      <i>recipe</i>
      <i>...</i>
</pre>

For example, in the following example, the ```all``` rule would run the corresponding pattern rule for ```objects```, and for each of ```main.o``` and ```helper.o``` in ```objects```, the target pattern would strip out the respective stems ```main``` and ```helper``` and apply it to the prerequisite pattern, resulting in the corresponding prerequisites ```main.c``` and ```helper.c```. Then each rule would be run, and their compile recipe would be executed, producing ```main.o``` and ```helper.o```:

```
OBJECTS = main.o helper.o

all: $(OBJECTS)

$(OBJECTS): %.o: %.c
        $(CC) -c $< -o $@
```

#### Using Functions

Functions have a multitude of uses in Makefiles. Some simple useful ones are:
- ```$(wildcard pattern)```: returns a a list of filenames that match the given pattern
- ```$(foreach var,list,text)```: sets ```var``` to the evaluated ```text``` for each word in ```list```
- ```$(if condition,true-part,false-part)```: returns ```true-part``` if ```condition``` is true, otherwise returns ```false-part```

#### Additional Tips

You can have ```make``` silently execute commands using the ```@``` symbol. For example the following:

```
all:
	echo Hello world
	@echo Hello world
```

Would not produce the second ```@echo Hello World``` command itself and only the output:

```bash
$ make all
>>> echo Hello world
>>> Hello world
>>> Hello world
```

## Managing Multiple Directories with Makefiles

Now you have the knowledge to write some more intermediate Makefiles. But how would you manage a larger project/library with many subdirectories? Well, you can use multiple Makefiles and run them all from your top Makefile in your main directory.

#### Calling Subdirectory Makefiles

```make``` has some internal utility variables. One of them is a reference to the ```make``` command itself, ```$(MAKE)```. You can use this variable to call sub-```make```s on other Makefiles in subdirectories using the ```-C``` option, which specifies the directory the Makefile is in. Usage would usually be in the following template:

<pre>
$(MAKE) -C <i>subdirectory</i>
</pre>

You can tell when ```make``` is entering another directory because it will automatically notify you when and where it is entering and exiting, as well as the sub-make depth. The messages would typically be in the following template:

<pre>
make[<i>depth</i>]: Entering directory '<i>directory</i>'
make[<i>depth</i>]: Leaving directory '<i>directory</i>'
</pre>

Another useful internal variable is ```$(PWD)```, which is like the shell command ```pwd``` that gets the current working directory.

#### Exporting Variables

You can explicitly communicate variable values from a top level make to a sub-```make``` in Makefiles using ```export```. These exported variables will be defined in the sub-```make``` by default, but will not override a variable that is explicitly defined in the Makefile of the sub-```make```. The typical usage would be in the template:

<pre>
export <i>variable ...</i>
</pre>

You can also export all the variables in the current Makefile by not specifying any variables:

<pre>
export
</pre>

If you want to specify any variables to not be exported, you can use ```unexport```:

<pre>
unexport <i>variable ...</i>
</pre>

#### Example Usage

Here is an example of how you could manage a simple multi-directory project. The project directory is as follows:

```
|-- debug
|   |-- debug.c
|   |-- debug.h
|   `-- Makefile
|-- include
|   |-- common.h
|-- main
|   |-- helper.c
|   |-- main.c
|   |-- main.h
|   `-- Makefile
`-- Makefile
```

The top directory Makefile is as follows:

```
MAKE_DIR = $(PWD)
MAIN_DIR    := $(MAKE_DIR)/main
DEBUG_DIR   := $(MAKE_DIR)/debug
INCLUDE_DIR := $(MAKE_DIR)/include

INC_SRCH_PATH := 
INC_SRCH_PATH += -I$(MAIN_DIR)
INC_SRCH_PATH += -I$(DEBUG_DIR)
INC_SRCH_PATH += -I$(INCLUDE_DIR)

CC = gcc

CFLAGS :=
CFLAGS += $(INC_SRCH_PATH)
CFLAGS += -Wall -O -DDEBUG

export MAKE_DIR CC CFLAGS INC_SRCH_PATH

all:
	@$(MAKE) -C main
	@$(MAKE) -C debug

.PHONY: clean
clean:
	@$(MAKE) -C main clean
	@$(MAKE) -C debug clean
```

And an example Makefile in the ```main``` subdirectory is as follows:

```
PROG = DEMO

SRCS = $(wildcard *.c)
OBJS = $(SRCS:.c=.o)

$(PROG): $(OBJS)
	@$(CC) $^ $(CFLAGS) -o $@
	@echo "  Generate Program $(PROG) from $^"

$(OBJS): $(SRCS)
	@$(CC) $(CFLAGS) -c $^
	@echo "  CC $(OBJS)"

.PHONY: clean
clean:
    @rm -f $(OBJS)
```

In the above example top directory Makefile, first the working directory is stored into variable ```MAKE_DIR```, and then used to create paths to the subdirectories. These subdirectories are all appended to the ```INC_SRCH_PATH``` variable. The ```CC``` variable is set to ```gcc```, and the ```CFLAGS``` variable appends ```INC_SRCH_PATH``` and some ```gcc``` flags. The ```MAKE_DIR CC CFLAGS INC_SRCH_PATH``` variables are then set to be exported to any sub-```make```s. The ```all``` and ```clean``` rules call sub-```make```s to the ```main``` and ```debug``` directories.  
In the Makefile in the ```main``` directory, the ```DEMO``` target program is built with the prerequisites of any object files in corresponding to the C source files, which need to be compiled first. We can see that exported```CFLAGS``` variable can be useful to pass in the paths for input links between the source files and the same flags consistently in the project, so ```gcc``` can compile properly.  

Some example output from the top directory would be:

```bash
$ make
>>> make[1]: Entering directory '.../main'
>>>   CC main.o helper.o
>>>   Generate Program DEMO from main.o helper.o
>>> make[1]: Leaving directory '.../main'
>>> make[1]: Entering directory '.../debug'
...
>>> make[1]: Leaving directory '.../debug'
```

## Advantages and Disadvantages to ```make``` and Makefiles

#### Advantages
- ```make``` is everlasting: It was first developed in 1976 and it's not going away any time soon. It provides a simple, standardized way to write projects that has stood the test of time, and is still widely used.
- ```make``` is platform independent: Makefiles specify the commands needed to build targets, and the commands themselves are usually shell commands or calls to compilers and interpreters that can be execute on different platforms. Additionally, with variables you can define commands for compilers and tools, as well as using conditional statements to change them based on environment variables or other conditions, making it easy to to switch compilers/tools based on the platform/environment.
- ```make``` make encourages you to record your code: The modular nature of Makefiles encourages you to record each step you make, enabling you and others to reliably reproduce the entire process. You are essentially mapping out a directed acyclic graph of your project with Makefiles.
- ```make``` allows for easy and reliable CI: By providing a Makefile with common ```make``` targets like ```build```, ```compile```, ```lint```, and ```test```, you can start writing your project  Your CI will execute your ```make``` targets, deleting your generated files and rebuilding from scratch to test. You can then utilize other more modern dependency managers or script runners under the hood.
- ```make``` functions off of timestamps: timestamps are built into approximately every filesystem, so you don't need to store extra metadata or do any further checks.

#### Disadvantages
- ```make```'s syntax is clunky and hard to learn: The [full manual](https://www.gnu.org/software/make/manual/html_node/index.html) is 183 pages and is not very pretty and not that intuitive, including whitespace sensitivity, where indentation errors are difficult to spot by simply looking. The built-in functions and constructs lack some complex logical capabilities and programming features that can be difficult to express in a Makefile.
- ```make``` functions off of timestamps: Rebuilding due to changes in timestamps can be unreliable/undesirable and inefficient when content is not changed.
- ```make``` platform independency writing can be difficult: Handling all the cases of which compilers and tools to use in cases for different platforms can be tedious and challenging.
- ```make``` error messages are not always clear: It can be difficult to identify and fix issues from the built-in error messages alone, especially in larger complex build systems.
- ```make``` doesn't easily address external dependencies: Managing source files dependencies is what ```make``` was built for, but third party library and package dependency management would require additional effort or external tools.

## Additional Resources
- The official GNU ```make``` documentation: https://www.gnu.org/software/make/manual/html_node/index.html
- A more detailed tutorial on Makefiles: https://github.com/Nuno-Jesus/Make-A-Make
- A simple Makefile example: https://github.com/remonbonbon/makefile-example/tree/master
- A more advanced Makefile managed project: https://github.com/skwee357/wrap-os/tree/master

## Footnotes

<a name="1"></a> [↩](#Recipe)1. The prefix for recipes can be changed by changing the .RECIPEPREFIX variable, for example the following is a valid makefile:
```
.RECIPEPREFIX = ~
hello:
~ @echo hello world
```

<a name="2"></a> [↩](#Running-a-Simple-Makefile)2. If you want to call make on a file with a different name, use the ```-f``` option, e.g. calling ```make``` on a file named foo.mk:
```
make -f foo.mk
```

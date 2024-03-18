# Introduction to Nano

## **What is Nano?**
Nano is a text editor for Unix-like computing systems or operating environments using a command line interface. It is simple and user-friendly, making it great for people who are beginners to using command line interfaces.

## **Installing Nano**
Nano text editor is pre-installed on macOS and most Linux distros. To check if it is installed on your system, type:

```nano --version```

If you don’t have nano installed on your system, you can install it using your distribution’s package manager.

#### Install Nano on Ubuntu and Debian
```sudo apt install nano```

#### Install Nano on CentOS and Fedora
```sudo yum install nano```

## Opening and Creating Files
To open an existing file or to create a new file, type nano followed by the file name:
```nano filename```

This will open a new editor window, and you can start editing the file. It should look something like this.
<img width="837" alt="Screenshot 2024-03-17 at 8 02 28 PM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/74018027/8e6a6e5c-c0dd-4e98-9485-208c66b00704">


At the bottom of the window, there is a list of the most basic command shortcuts to use with the nano editor. All commands are prefixed with either ^ or M. ^ represents the Ctrl key. For example, the ^J commands mean to press the Ctrl and J keys at the same time. M represents the Alt key. To get a list of all commands, type Ctrl+g.

To open a file, you must have read permissions to the file.

If you want to open a file with the cursor on a specific line and character, use the following syntax:

```nano +line_number,character_number filename```

If you do not include the character_number the cursor will be positioned on the first character.

Additional Resources
https://www.nano-editor.org/dist/v2.2/nano.html

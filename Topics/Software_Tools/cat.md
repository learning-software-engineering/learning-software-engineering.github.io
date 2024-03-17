# The 'cat' Command Guide

## Introduction to the `cat` Command

The `cat` (concatenate) command is a staple in Unix and Unix-like operating systems for displaying, concatenating, and writing file contents to the standard output.

## Syntax

```bash
cat [OPTION]... [FILE]...
```

- `[OPTION]`...: Modify the behavior of `cat`.
- `[FILE]`...: Files to be processed. Reads from stdin if no file or `-` is specified.

## Common Options

- `-n`, `--number`: Number all output lines.
- `-b`, `--number-nonblank`: Number non-empty output lines only.
- `-s`, `--squeeze-blank`: Squeeze multiple adjacent blank lines.
- `-E`, `--show-ends`: Display `$` at the end of each line.
- `-T`, `--show-tabs`: Display TAB characters as `^I`.

## Displaying File Contents

To display the contents of a file:

```bash
cat file.txt
```

<img width="363" alt="Screenshot 2024-03-11 at 11 28 56 PM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/98674104/2504e6f6-a0cf-4e13-a1eb-5ae9f0412acd">

## Concatenating Files

To concatenate multiple files into one:

```bash
cat file1.txt file2.txt > combined.txt
```

<img width="528" alt="Screenshot 2024-03-11 at 11 49 17 PM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/98674104/2850772a-6e3d-4dd5-af35-e97b8a985413">

## Creating Files

To create a new file:

```bash
cat > newfile.txt
```

## Appending to Files

To append text to an existing file:

```bash
cat >> existingfile.txt
```

<img width="452" alt="Screenshot 2024-03-12 at 12 00 29 AM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/98674104/4c3bc972-8242-4de0-8a1d-d869656630ec">

<img width="348" alt="Screenshot 2024-03-12 at 12 01 00 AM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/98674104/40153a7b-bf24-4d8d-ad0a-35cb4f93c26c">

## Viewing Non-Printing Characters

To view end-of-line or tabs:

```bash
cat -E file.txt
cat -T file.txt
```

## Reading Standard Input

You can use cat without specifying a file to read from the standard input. This is useful for quickly creating file content from terminal input:

```bash
cat > example.txt
Type your content here...
Press CTRL+D (EOF) to save and exit.
```

## Viewing Multiple Files

cat can also be used to view the contents of multiple files sequentially on the terminal. This is a quick way to compare or merge files manually:

```bash
cat file1.txt file2.txt file3.txt
```

<img width="502" alt="Screenshot 2024-03-12 at 12 03 41 AM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/98674104/3be8397f-788d-4394-b2a2-438f83bbc4f9">

## Sort and Remove Duplicate Lines

If you have a file with list items or entries that you want to sort and remove duplicates from, you can use cat in combination with other commands like `sort` and `uniq`.

```bash
cat list.txt | sort | uniq > sorted_list.txt
```

Using `cat list.txt | sort | uniq > sorted_list.txt` streamlines the process of organizing data by automatically sorting the contents of `list.txt`, removing any duplicate entries, and saving the cleaned, ordered list to `sorted_list.txt`. This command sequence accelerates workflows by performing data cleanup and organization in a single step, eliminating the need for manual sorting and deduplication, thus saving time and reducing potential for error in data handling.

## Conclusion

The `cat` command is an essential tool for text processing in Unix/Linux environments, offering a wide range of functionalities from file display to concatenation and debugging.

## Reference

https://www.geeksforgeeks.org/cat-command-in-linux-with-examples/

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

## Concatenating Files

To concatenate multiple files into one:

```bash
cat file1.txt file2.txt > combined.txt
```

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

## Conclusion

The `cat` command is an essential tool for text processing in Unix/Linux environments, offering a wide range of functionalities from file display to concatenation and debugging.

## Reference

https://www.geeksforgeeks.org/cat-command-in-linux-with-examples/

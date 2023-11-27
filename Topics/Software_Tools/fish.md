# A fin-troduction to `fish`

## Introduction

### enter `fish`!

...the **f**riendly **i**nteractive **sh**ell.

fish offers a command-line interface that is focused on usability and interactive use[^1].

This introduction will be less about the syntax differences between the fish language
and bash or zsh and more about the out-of-the-box features that are offered from this shell.

### A dish served best straight out of the oven

Some of you might be familiar with zsh plugin managers such as
[oh-my-zsh](https://ohmyz.sh/) that can configure zsh to your liking, but fish
just works. No more messing with chunky zsh configs and slow shells that make
you wait several hundred milliseconds to type another command.

### Installation

It's recommended to check the [fish homepage](https://fishshell.com/) for up-to-date
instructions for installing the latest version of fish on your platform.

## Syntax highlighting

fish performs syntax highlighting as you type. Invalid or non-existent, unexecutable
commands appear red if they cannot be executed. On the contrary, valid commands will
appear in a different color.

## Autosuggestions

fish suggests commands as you type, based on command history. As you type commands,
suggestions are offered after the cursor in gray. To accept the suggestion, press
`→` or `Control`+`F`.

<img width="280" alt="autosuggestions" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/40929644/fd505f17-4265-41ac-b41f-59bbdd0eb670">


## Autocompletions

fish comes built with many autocompletions for commands you will encounter often.
It also parses man pages and automatically generates completions.

## Tab completion

When you type `Tab`, fish guesses the rest of the word under the cursor. It suggests
a number of possibilities and opens a menu (or "pager") that allows you to select
the command you're looking for.

## A `Control`+`R` for the future

This is a command that you might find yourself using a lot! In bash or zsh, to
search your history, you can use `Control`+`R` to find some commands you've used
previously. With fish, you can type a substring, such as 'alac', and press
`↑` and `↓` (or `Control`+`P` and `Control`+`N`) to traverse commands in your
history containing 'alac'. You can also use ctrl+r as usual and this opens a pager
to search your history.

## Default shell

At this point, if you are convinced with the benefits of fish, you can change
your login shell to it as follows:

1. Add the shell to `/etc/shells/`:

```bash
$ echo /usr/local/bin/fish | sudo tee -a /etc/shells
```

2. Change your default shell:

```bash
$ chsh -s /usr/local/bin/fish
```

## Plugins

First -- yes, this post starts with saying fish works out of the box, and it does!
You could stop right before this section and be happy with your new found shell.

But there's just one plugin to fish to leave you with: [Tide](https://github.com/IlanCosman/tide).
Its most useful feature is that it enables asynchronous rendering, making the
prompt instantly responsive.

## References

[^1]:https://fishshell.com/docs/current/index.html

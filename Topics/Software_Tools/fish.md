# A fin-troduction to `fish`

## Introduction

### enter `fish`!

...the **f**riendly **i**nteractive **sh**ell. A shell is a program that starts other programs 
(you might have installed `bash` or `zsh`). fish offers a command-line interface that is focused on usability and interactive use[^1].

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
commands appear red if they cannot be executed.

<img width="101" alt="gus" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/40929644/69c96e62-5404-4f37-840e-1bbdffcb6538">

On the contrary, valid commands will appear in a different color.

<img width="101" alt="git" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/40929644/46110031-e0e2-4522-b630-791f9c387005">

## Autosuggestions

fish suggests commands as you type, based on command history. As you type commands,
suggestions are offered after the cursor in gray. To accept the suggestion, press
`→` or `Control`+`F`.

<img width="280" alt="autosuggestions" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/40929644/fd505f17-4265-41ac-b41f-59bbdd0eb670">

## Autocompletions

fish comes built with many autocompletions for commands you will encounter often.
It also parses man pages and automatically generates completions.

<img width="840" alt="autocompletions" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/40929644/7aa5d9fc-021a-48a8-9f20-823e666a068c">

## Tab completion

Many shells offer tab completion, but fish provides a modern interface out of the box.
When you type `Tab`, fish guesses the rest of the word under the cursor. It suggests
a number of possibilities and opens a menu (or "pager") that allows you to select
the command you're looking for.

<img width="840" alt="tab" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/40929644/2a4c924f-d3a8-4205-8480-d541839b923d">

## A `Control`+`R` for the future

This is a command that you might find yourself using a lot! In bash or zsh, to
search your history, you can use `Control`+`R` to find some commands you've used
previously. With fish, you can type a substring, such as 'alac', and press
`↑` and `↓` (or `Control`+`P` and `Control`+`N`) to traverse commands in your
history containing 'alac'. 

<img width="280" alt="substr-updown" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/40929644/1c616bac-6071-460f-89c5-a4f73450a05d">

You can also use `Control`+`R` as usual and this opens a pager to search your history.

<img width="308" alt="ctrlr" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/40929644/1b4feb10-44c0-4a78-b33e-aca7dd54de79">

### And for some privacy...

Prefixing the command-line with a space prevents the line from being stored in
history. This can be useful if your command contains a secret token that you don't want
to be stored on disk.

## Flying through directories

If you've ever used `pushd` or `popd`, you won't have to ever again! Using `Alt`+`→`
or `Alt`+`←`, you can traverse through directories you've previously changed to.

## A note on POSIX compliance

fish isn't POSIX compliant, but it isn't designed to be! Typing `bash` into the
command-line to execute a command or running a script opening with a hashbang are
always options if you need bash.

## Default shell

At this point, if you're convinced with the benefits of fish, you can change
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

First — yes, this post starts with saying fish works out of the box, and it does!
You could stop right before this section and be happy with your new found shell.

But there's just one plugin to fish to leave you with: [Tide](https://github.com/IlanCosman/tide).
Its most useful feature is that it enables asynchronous rendering, making the
prompt instantly responsive.

## Resources

- [fish docs](https://fishshell.com/docs/current/index.html)
- [fish language](https://fishshell.com/docs/current/language.html)
- [Tide prompt](https://github.com/IlanCosman/tide)
- [An example fish shell workflow from devaslife](https://www.youtube.com/watch?v=KKxhf50FIPI)

## References

[^1]:https://fishshell.com/docs/current/index.html

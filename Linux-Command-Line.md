# Linux Command Line Notes

***

## Introduction

* Unix is an operating system developed at Bell Labs in the mid 1960s
* Unix is the 'grandfather' of many OS
* In the early days of computers, OS were tightly tied to specifc hardware. Unix decoupled the two and was easily portable to other hardware
* Philosophy of Unix
  * Write programs that do one thing and do it well
  * Write programs to work together
  * Write programs to handle text streams, becasue it is a universal interface
* True UNIX
  * Today, "UNIX" is a trademark of a global consortium called The Open Group
  * They maintain a set of standards called the Single UNIX Specification
* Unix-like
  * OS are based on the original Unix OS and are compatible with the Unix standards, but cannot legally use the UNIX name
* Linux
  * "Free Unix"
  * Linus's kernel + GNU components
* Shell
  * A shell is a computer interface to the OS
  * Shell exposes the OS's services to human users or other programs
  * Shell takes our commands and gives them to the OS to perform
* Terminal
  * A terminal is a program that runs a shell
  * Originally, terminals were physical devices
* Bash
  * On most Linux-based systems, the default shell program is `bash`

***

## Basics

* Command Structure

  * ```bash
    command -options arguments
    ```

  * Most commands support multiple options that modify their behaviours

  * Options can be combined with single `-`

  * Long-form options

    * Some options support equivalent long-form options that are usually two words and prefixed with two dashes instead of just one
    * Long term options cannot be combined

  * Arguments are the values we provide to commands

  * Options that require arguments can omit the space between option and argument

  * **Case matters!**

  * `date`

  * `ncal`

  * `cal`

* Man Page

  * `man <command>`
  * Man page is displayed using `Less`
  * Man page synopsis
    * Anything listed inside of square brackets `[]` is OPTOINAL
  * Manual sections
    1. User Commands
    2. System Calls
    3. C Library Functions
    4. Special Files
    5. File Forms
    6. Games
    7. Miscellaneous
    8. System Admin Commands

* Type of commands

  * An executable program
    * Usually stored in `/bin`, `/usr/bin`, `/usr/local/bin`
    * These are compiled binary files
  * A built-in shell command
  * A shell function
  * An alias
  * `type`
    * Check the command's type
  * `which`
    * Located a program file in the user's path

***

## Navigation

* Directories
  * Root directory: `/`
  * Users (Home) directory: `~` or `/users` or `/home`
  * Binaries directory: `/bin`
    * Contains executable programs
  * `/etc`
    * Contains configuration files and initialisation scripts
  * `/var`
    * Contains files related to logging
  * `/usr`
    * Contains files related to user installation
* `pwd`
  * Print working directory name
* `ls`
  * List directory contents
  * Common options
    * `-l`: prints in long list formats
    * `-a`: lists any hidden files that begin with `.`
* `cd <directory>`
  * Change directory
  * Current directory: `.`
  * Parent directory: `..`
  * Relative and absolute path

***

## Creating Files & Folders

* `touch <filename>`
  * Change file access and modification times; if any file doesn't exist, it is created with default permissions
* `file <filename>`
  * Determine file type
  * OS doesn't't use the file extension to decide on the file type.
  * File extension decides which application to be used to open the file
* `mkdir <folderName>`
  * Make directories
  * Common options
    * `-p`: create intermediate deirectories as required

***

## Nano

* Nano is a simple text editor that we can access right from terminal
* Some others: vim, emacs, etc.
* `nano <fileName>`
  * Use shortcuts to perform tasks

***

## Deleting, Copying & Moving

* `rm <fileName>`
  * Remove files or directories
  * `rm` **DELETE** files, there is no undo or recycle bin to retrieve them from
  * Common options
    * `-d`: remove empty directories
    * `-r`: remove directories and their contents recursively
    * `-i`: prompt before every removal
    * `-f`: never prompt
* `mv <source> <destination>`
  * Move files
* `mv <source> <target>`
  * Rename the file or directory if the last argument does not name an existing directory
* `cp <source> <destination>`
  * Copy files
  * Common options
    * `-r`: copy directories recursively

***

## Shortcuts

* `^L`: clear
* `^A`: move the cursor to the beginning of the line
* `^E`: move the cursor to the end of the line
* `option ->`: move the cursor forward one word
* `option <-`: move the cursor backward one word
* `^T`: swap character with its previous
* `^K`: kill the text from the current cursor location to the end of the line
* `^U`: kill the text from the current cursor location to the beginning of the line
* `option D`: kill the text from the current cursor location throught the end of the word
* `^Y`: retrieve the most recently killed text
* `history`: view the recorded commands stored in `~/.bash_history`
  * `!<number>`: re-run the No.number command in the history
  * `^R`: search commands with the best matches

***

## Working with Files

* `cat [fileName ...]`
  * Concatenate and print files
* `less [fileName]`
  * Display the content of a file one page at a time. Navigate forward and backward is feasible
* `tac [fileName ...]`
  * Concatenate and print files in "vertical" reverse
* `rev [fileName ...]`
  * Reverse lines of a file (horizontally)
* `head [fileName ...]` `tail [fileName ...]`
  * Display first / last lines of files
  * Common options
    * `-n count`: print `count` lines
      * Or just `-count`
    * `-c bytes`: print `bytes` bytes
    * `tail -f`
      * Causes tail to not stop when end of file is reached, but rather to wait for additional data to be appended to the input
      * Useful for logs
* `wc [fileName ...]`
  * Line, word, character, byte count
  * `-l`, `-w`, `-c`
* `sort [fileName ...]`
  * Print sorted content of a file (doesn't change the file)
  * Common options
    * `-r`: in reverse order
    * `-n`: sort numerically
    * `-u`: unique only

***



## References

* [Article on Unix History](https://spectrum.ieee.org/the-strange-birth-and-long-life-of-unix)
* [Operating System Family Tree](https://eylenburg.github.io/os_familytree.htm)
* 
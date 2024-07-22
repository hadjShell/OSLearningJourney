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

## Searching

* `locate`
  * Search pathnames across the machine that match a given substring and then prints out any matching names
  * Use a pre-generated database file
    * `sudo updatedb`
      * Update database manually
  * `-e`
    * Print entries that actually exist at the time `locate` is running
  * `-i`
    * Ignore case
  * `-l`
    * Limit the number of entries
* `find`
  * By default, it lists every single file and directory nested in the current directory
  * Or provide a specific folder
  * Doesn't use a database file
  * `-type f`
    * Only looks for files
  * `-type d`
    * Only looks for directories
  * `-name "*.txt"`
    * Find by a pattern
    * `-iname`
      * Ignore case
  * `-size +2G`
    * Find by size
  * `-user david`
    * Find by user
  * `-empty`
  * `-mmin`, `-cmin`, `-amin`, `-mtime`, `-ctime`, `-atime`, `-newer`, `-cnewer`, `-anewer`
    * Find by last modification time, last changed time, recent access time
  * `-and`, `-or`, `-not`
  * `find -exec command '{}' ';'`
    * Perform actions on each matching pathname
    * `{}` are a placeholder for the current pathname (each match)
    * `;` indicate the end of the command

***

## `grep`

* `grep PATTERN FILE` 
  * Search for patternin each files's content, print each line that matches a pattern
  * Support regex
  * `-i`
    * Ignore case
  * `-w`
    * Word search
  * `-r`
    * Recursive search which includes all files under a directory
    * If we don't specify a directory, it will search current working directory
  * `-c`
    * Count the matches
  * `-A2`, `-B2`, `C2`
    * Print lines after or before or both the match lines
  * `-n`
    * Line number

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

## Nano

* Nano is a simple text editor that we can access right from terminal
* Some others: vim, emacs, etc.
* `nano <fileName>`
  * Use shortcuts to perform tasks

***

## Redirection

* Standard streams
  * The three standard streams are communication channels between a computer program and its environment
* Standard output
  * Standard output is a place to which a program or command can send information
  * The information could go to a screen to be displayed; to a file; or even to a printer or other devices
  * By default it goes to the terminal window
* Standard error
  * Commands and programs also have a destination to send error messages
  * By default, the shell directs the error message to the screen
* Standard input
  * Standard input is where a program or a command gets its input information from
  * By default, the shell directs standard input from the keyboard
  * The input information could come from a keyboard, a file, or from another command
* Redirection
  * Redirection describes the ways we can alter the source of standard input, and the destinations of standard output and standard error
  * Redirect stdout
    * `command > filename`
      * Overwrite
    * `command >> filename`
      * Append
  * Redirect stdin
    * `command < filename`
  * Redirect stderr
    * `wrong_command 2> filename`
    * `wrong_command 2>> filename`

***

## Piping

* Pipes are used to redirect a stream from one program to another program
* `command1 | command2`
  * The stdout of the first command will be passed to the stdin of the second command
* `command1 | tee file.txt | command2`
  * `tee` reads stdin and copies it both to stdout and to a file
* `xargs`
  * Takes stdin into a bundle that will be provide as an argument list to the next command

***

## Expansion

*  `*`
  * Represents 0 or more characters in a filename
* `?`
  * Represents a single character
* `[]`
  * Specify a range of characters to match
  * Range: `[0-9]`
* `[^]`
  * Complement range
* `~`
* `{}`
  * Generate arbitrary strings
  * Range: `{a..c}`
  * Change interval: `{2..10..2}`
* `$((expression))`
  * Arithmetic expansion
* `$(command)`
  * Display the output of another command
* `""`
  * If we wrap text in double quotes, the shell will respect our spacing and will ignore special character except for `$`, `\`, `backtick`
* `''`
  * Suppress all forms of substitution

***

## Permission

* Unix and Unix-like systems are multi-user systems
* A single user may be the owner of files and directories, meaning that he has control over their access
* Users can belong to groups which are given access to particular files and folders by their owners
* File attributes
  * 10 characters
  * Type of the file + read, write, execute permissions for the file owner + for the group owner + for everyone else
  * Type of the file
    * `-` regular file
    * `d` directory
    * `l` symbolic link
    * `c` character devices
    * `b` block devices
* `chmod mode file`
  * Change the permissions of a file or a directory
  * Symbolic notation
    * `[ugoa][+-=][rwx]`
      * `=` set a permission and remove others
  * Octal notation
    * `[0-7][0-7][0-7]`
* `su - username`
  * Substitute user a new login session
  * Type `exit` to leave the session
* `sudo command`
  * Execute a command as the root user
* `chown USER[:GROUP] FILE(s)`
  * Change the owner and/or the group owner of a file or directory
* `groups USER`
  * Check user's group
* `addgroup GROUPNAME`
* `adduser USER GROUP`

***

## Environment

* The shell maintains a set of information during a shell session, known as the environment
* A series of key-value pairs
  * Your home directory
  * Your working directory
  * The name of your shell
  * The name of the logged in user
  * Etc.
* `printenv`
* `$ENV_VAR`
  * Parameter expansion
* `var=value`
  * Define custom shell variables
  * Only accessible in current shell session
  * Good to use lower case
* `export var=value`
  * Define custom environment variables
  * Accessible in child processes, lost in a new terminal window
* `bash`
  * Start a new session
* Start-up files
  * When we log in, the sehll reads information from startup files
  * First, the shell reads from global config files that effect the environment for all users
  * Then, the shell reads startup files for specific users
    * For login session
      * `/etc/profile` global config for all users
      * `~/.bash_profile` user's personal config
      * `~/.bash_login` read if previous file is not found
      * `~/.profile` read if previous twp are not found
    * For non-login session (a new terminal window)
      * `/etc/bash.bashrc` global config
      * `~/.bashrc` specific config for each user (where we can define our own configs)
* Alias
  * Define our own commands
  * `alias ll="ls -l"`
  * Can be stored in a separate file `~/.bash_aliases`

***

## Bash Scripts

* Basic steps
  * Write a script in a file and save it
  * Make the script executable using `chmod`
  * Verify that shell can find your script
* The first line of our script should read `#!PATH`
  * Tell the OS which interpreter it should use when parsing this file
* `PATH` variable
  * When we run a command, the shell starts looking for the executable program in the list of directories stored in the `PATH` variable

***



## References

* [Article on Unix History](https://spectrum.ieee.org/the-strange-birth-and-long-life-of-unix)
* [Operating System Family Tree](https://eylenburg.github.io/os_familytree.htm)
* 
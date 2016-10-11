# Working with commands
### What exactly are commands?
it can be one of four things:
-  **An executable program** : like all those files we saw in /usr/bin. such as C,C++,python,ruby,perl.

- **A command built into the shell itself.**

- **A shell function.**

- **An alias.**

### Identifying commands

- #### type - display a command's type

  ```
  type command
  ```
The `type` command is a shell builtin that displays the kind of command the shell will
execute, given a particular command name.

- #### which - display an executable's location

  ```
  which command
  ```


  `which` only works for executable programs, not builtins nor aliases that are substitutes for actual executable programs.

### Getting a command's documentation

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

- #### help - get help for shell buildins
  ```
  help command
  ```

- #### --help - display usage information

  ```
  command --help
  ```

- #### man - display a program's manual page
  ```
  man command
  ```
  On most Linux systems, man uses less to display the manual page, so all of the familiar
  less commands work while displaying the page.

  man page organization:

| section | contents |
| ------- | -------- |
| 1 | User commands |
| 2 | Programming interfaces for kernel system calls |
| 3 | Programming interfaces to the C library |
| 4 | Special files such as device nodes and drivers |
| 5 | File formats |
| 6 | Games and amusements such as screen savers |
| 7 | Miscellaneous |
| 8 | System administration commands |


  to specify a section number, use:
  ```
  man section search_item
  ```

- #### apropos - display appropriate commands

  ```
  apropos command
  ```
- #### what - display a very brief description of a command
  ```
  whatis command
  ```
- #### info - for GUI mainly
  ```
  info command
  ```

- #### other documentation files

  Many software packages installed on your system have documentation files residing in the /usr/share/doc directory.

### creating your own commands with alias
To put more than one command on a line,  separate each command with a semicolon character.
```
command1; command2; command3...
```

to create a alias:
```
alias name='string'
```
for example:
```
alias foo='cd; ls; cd -'
```

to remove an alias:
```
unalias name
```
to list all the aliases defined in the environment:
```
alias
```

# What is the shell?
#### return to [Contents](README.md)
### Concept
The shell is a program that takes keyboard commands and passes them to the operating system to carry out.

* Almost all Linux distributions  supply a shell program called bash.
* bash : Bourne again shell,a reference to the fact that bash is an enhanced replacement for sh,the origial Unix shell program written by Bourne.

### Terminal emulators
Access to the shell.
* KDE(OpenSUSE) use **konsole**
* GNOME(Ubuntu,Centos) use **gnome-terminal**

### Command history
Use *up-arrow* to get the previous command.
Press *down-arrrow*,the previous command disappears.

**Note : Most Linux distributions remember the last 1000 commands by default.**

### Cursor movement
`ctrl-C` or `ctrl-V` is not worked for copying and pasting inside a terminal window.

**Note : Setting the focus policy to "focus follows mouse" in the Configuration program for your window manager.**

### Some simple commands
```
$ date
$ cal
$ df
$ free
```
* `date`: display the current time and date.
* `cal`: display a calendar for current month.
* `df` : display the current amount of free space in your disk drives.
* `free` : display the free memory.

### Exiting a terminal
```
$ exit
```
> The console behind the Curtain:

>Even if no terminal emulator running,several terminal sessions continue to run behind the graphical desktop,called **virtual terminal** or **virtual consoles**.

* `ctrl-alt-F1` through `ctrl-alt-F6` to access.
* `alt-F1` through `ctrl-F6` to switch from one virtual terminal to another.
* `alt-F7` to return to the graphical desktop.

#### return to [Contents](README.md)

# Exploring the system
### More fun with `ls`
* specify the current working directory to list:
```
$ ls
```

* specify the directory to list:
```
$ ls /home
```

* specify multiple directories
```
$ ls ~ /usr
```
list both the user's home directory and the /usr directory.

##### Options and arguments

option | long option | description
------ | ----------- | -----------
-a     | -all | List all files,even files that are hidden.
-A | --almost all | Like the -a,except it does not list .(current directory) and ..(parent directory).
-l | | display results in long format.
-r | --reverse | display the results in reverse order.Normaally,ls displays its results in *ascending* alphabetical order.
-S | | sort results by file size.
-t | | sort by modification tme.

### Determining a file's type with file
```
$ file filename
```

### Viewing file with less
There are many ways to represent information on a computer.One of the eariest and simpliest is ASCII(short for American Standard Code for Information Interchange)
```
$ less filename
```
**less commands:**

command | Action
------- | ------
G | Move to the end of the file
1G or g | Move to the beginning of the file
n | search for the next occurrence of the previous search
h | Display help screen
q | Quit less

**Less is more:**
Less was designed as an improved replacement of an earlier Unix program called *more*.

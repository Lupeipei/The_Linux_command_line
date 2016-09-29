# Navigation

### Hierarchical directory structure

Unix-like systems like Linux always have a single file system tree. It organizes its files in what is called a **hierarchical directory structure**.

### The current working directory
```
$ pwd
```
### Listing the contents of a directory
```
$ ls
$ ls -a
```
More details about `ls` in the later chapters.

### Changing the current working directory
There are two kinds of pathnames,**absolute pathnames** and **relative pathnames**.
* absolute pathnames : begins with the root directory
* relative pathnames : starts from the working directory,it uses `.` or `..` to represent relative positions in the file system trees.


**Relative pathnames** is perferred,cause it requires the least typing! :)

e.g.
```
$ cd /usr/bin
$ cd ..
$ cd ./bin 
```
* `cd` : changes the working directory to your home directory.
* `cd .` : refers to the working directory
* `cd ..` : refers to the working directory's parent directory.

**Note :**
* Files and Commands are case-sensitive.

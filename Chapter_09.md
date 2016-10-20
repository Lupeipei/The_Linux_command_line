# Premissions

### Owners, Group Members, And Everybody Else
Using `id` to find out information about your identity:

```
id
output: uid=500(me) gid=500(me) groups=500(me)
```
- uid: user id;
- gid: a primary group id.

superuser's id is 0.

**Note:**
- Fedora starts its numbering of regular user accounts at 500, while Ubuntu starts at 1000.

- User accounts are defined in the */etc/passwd* file and groups are defined in the */etc/group* file. When user accounts and groups are created, these files are modified along with */etc/shadow* which holds information about the user's password.

- Modern Linux practice is to create a unique, single-member group with the same name as the user.

### Reading, Writing, And Executing

Access rights to files and directories:
- read
- write
- execution

Using `ls` to get some clues.
```
ls -l foo.txt
output : -rw-r--r--  1 lucia  staff  1643 Oct  7 09:15 Chapter_01.md
```
The **first ten characters** of the listing are the **file attributes**. The first of these characters is **the file type**.

| Attribute | File Type |
| --------- | --------- |
| - | A regular file.|
| d | A directory.|
| l | A symbolic link. Notice that with symbolic links, the remaining file
attributes are *always “rwxrwxrwx” and are dummy values*. The real file attributes are those of the file the symbolic link points to. |
| c | A character special file. This file type refers to a device that handles data as a stream of bytes, such as a terminal or modem. |
| b | A block special file. This file type refers to a device that handles data in blocks, such as a hard drive or CD-ROM drive. |

The remaining nine characters of the file attributes, called the **file mode**, represent the read, write, and execute permissions for the file's owner, the file's group owner, and everybody else:

| Owner | Group | world |
| ----- | ----- | ----- |
| rwx | rwx | rwx |

Permissions attributes:

| Attribute | Files | Directories |
| --------- | ----- | ----------- |
| r | Allows a file to be opened and read. | Allows a directory's contents to be listed if the execute attribute is also set. |
| w | Allows a file to be written to or truncated,  however this attribute does not allow files to be renamed or deleted. The ability to delete or rename files is determined by directory attributes. | Allows files within a directory to be created, deleted, and renamed if the execute attribute is also set. |
| x | Allows a file to be treated as a program and executed. Program files written in scripting languages must also be set as readable to be executed. | Allows a directory to be entered, e.g. `cd directory`.|

#### chmod – Change File Mode

 `chmod` supports two distinct ways of specifying mode changes:
 - octal number representation;

 - symbolic representation.

---
CS concept learning:

**Octal (base 8)**, and its cousin, **hexadecimal (base 16)** are number systems often used to express numbers on computers.

Computers, on the other hand, were born with only one finger and thus do all all their counting in binary (base 2).


In octal, counting is done with the numerals zero through seven, like so:

0, 1, 2, 3, 4, 5, 6, 7, 10, 11, 12, 13, 14, 15, 16, 17, 20, 21...

Hexadecimal counting uses the numerals zero through nine plus the letters “A” through “F”:

0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F, 10, 11, 12, 13...

These days, hexadecimal notation (often spoken as “hex”) is more common than octal.

---

File Modes In Binary And Octal:

| Octal | Binary | File Mode |
| ----- | ------ | --------- |
| 0 | 000 | --- |
| 1 | 001 | --x |
| 2 | 010 | -w- |
| 3 | 011 | -wx |
| 4 | 100 | r-- |
| 5 | 101 | r-x |
| 6 | 110 | rw- |
| 7 | 111 | rwx |

an example:
```
> foo.txt
ls -l foo.txt
output : -rw-r--r--  1 lucia  staff  0 Oct 19 23:21 foo.txt
chmod 600 foo.txt
ls -l foo.txt
output : -rw-------  1 lucia  staff  0 Oct 19 23:21 foo.txt
```

You will usually only have to use a few common ones:

**7 (rwx), 6 (rw-), 5 (r-x), 4 (r--), and 0 (---).**

chmod Symbolic Notation:

| Symbol | Meaning |
| ------ | ------- |
| u | short for user but means the file and directory owner |
| g | Group owner |
| o | Short for “others,” but means world. |
| a | Short for “all.” The combination of “u”, “g”, and “o”. |

If no character is specified, “all” will be assumed.

- The operation “+” indicates that a permission is to be added;

- a “-” indicates that a permission is to be taken away

- a “=” indicates that only the specified permissions are to be applied and that all others are to be removed.

chmod Symbolic Notation Examples:

| Notation | Meaning |
| -------- | ------- |
| u+x | Add execute permission for the owner |
| u-x | Remove execute permission from the owner |
| +x | Add execute permission for the owner, group, and world.Equivalent to a+x. |
| o-rw | Remove the read and write permission from anyone besides the owner and group owner. |
| go=rw | Set the group owner and anyone besides the owner to have read and write permission. If either the group owner or world previously had execute permissions, they are removed. |
| u+x,go=rx | Add execute permission for the owner and set the permissions for the group and others to read and execute. Multiple specifications may be separated by commas. |

#### Setting File Mode With The GUI

In both Nautilus (GNOME) and Konqueror (KDE), right-clicking a file or directory icon will expose a properties dialog.

#### Set Default Permissions

The `umask` command controls the default permissions given to a file when it is created.

# A gentle introduction to vi

---
It takes years of practice.

But it is worth it.

Learning to use vim on a regular basis will pay off in the long run.

---
### Why We Should Learn vi

- Vi is always available.

- Vi is lightweight and fast.

- We don't want other Linux and Unix users to think we are sissies.

### A Little Background

The first version of vi was written in 1976 by Bill Joy, a University of California at Berkley student who later went on to co-found Sun Microsystems.

Most Linux distributions don't include real vi; rather, they ship with an enhanced replacement called vim (which is short for “vi improved”) written by Bram Moolenaar.

### Starting And Stopping vi

```
vim
```

```
:q
:q!
```

Tips:

- If you get “lost” in vi, try pressing the **Esc** key twice to find your way again.

### Edit Modes

vi is a modal editor. When vi starts up, it begins in command mode.

#### Entering Insert Mode

press "i" key.

press the Esc key to exit insert mode .

#### Saving work
```
:w
```

Tips:

- If you read the vim documentation, you will notice that (confusingly) command mode is called normal mode and ex commands are called command mode.

#### Moving the cursor around

| key | Moves The Cursor |
| --- | ---------------- |
| l or right arrow | Right one character. |
| h or Left Arrow | Left one character. |
| j or Down Arrow | Down one line. |
| k or Up Arrow | Up one line. |
| 0 (zero) | To the beginning of the current line. |
| ^ | To the first non-whitespace character on the current line. |
| $ | To the end of the current line. |
| w | To the beginning of the next word or punctuation character. |
| W | To the beginning of the next word, ignoring punctuation characters. |
| b | To the beginning of the previous word or punctuation character. |
| B | To the beginning of the previous word, ignoring punctuation characters. |
| Ctrl-f or Page Down | Down one page. |
| Ctrl-b or Page Up | Up one page. |
| numberG | To line number. For example, 1G moves to the first line of the file. |
| G | To the last line of the file. |


By prefixing a command with a number, we may specify the number of times a command is to be carried out. For example, the command “5j” causes vi to move the cursor down five lines.

### Basic Editing

#### Appending Text

-  vi offers a shortcut to move to the end of the current line and start appending. It's the “A” command.

- vi provides a command to append text, the sensibly named “a” command.

#### Opening A Line

- o : The line below the current line.

- O : The line above the current line.

#### Deleting Text

| Command | Deletes |
| ------- | ------- |
| x | The current character. |
| 3x | The current character and the next two characters. |
| dd | The current line. |
| 5dd | The current line and the next four lines. |
| dW |  From the current cursor position to the beginning of the next word. |
| d$ | From the current cursor location to the end of the current line. |
| d0 | From the current cursor location to the beginning of the line. |
| d^ | From the current cursor location to the first non- whitespace character in the line. |
| dG | From the current line to the end of the file. |
| d20G | From the current line to the twentieth line of the file. |

Note:

Real vi only supports a single level of undo. vim supports multiple levels.

#### Cutting, Copying, And Pasting Text

The y command is used to “yank” (copy) text.

| Command | Copies |
| ------- | ------- |
| yy | The current line. |
| 5yy | The current line and the next four lines. |
| yW |  From the current cursor position to the beginning of the next word. |
| y$ | From the current cursor location to the end of the current line. |
| y0 | From the current cursor location to the beginning of the line. |
| y^ | From the current cursor location to the first non- whitespace character in the line. |
| yG | From the current line to the end of the file. |
| y20G | From the current line to the twentieth line of the file. |

 the P command to paste the contents.

#### Joining lines
J (not to be confused with j, which is for cursor movement) to join lines together.

### Search-And-Replace

#### Searching Within A Line
The f command searches a line and moves the cursor to the next instance of a specified character.

- For example, the command fa would move the cursor to the next occurrence of the character “a” within the current line.

#### Searching The Entire File
```
/search_word
```
type n to get the next matches.

note: vi allows the use of regular expressions.

### Global Search-And-Replace

To change the word “Line” to “line” for the entire file, using :

```
:%s/Line/line/g
```

An example of global search-and-replace syntax:

| Item | Meaning |
| ---- | ------- |
| : | The colon character starts an ex command. |
| % | Specifies the range of lines for the operation. % is a shortcut meaning from the first line to the last line. Alternately, the range could have been specified 1,5 (since our file is five lines long), or 1,$ which means “from line 1 to the last line in the file.” If the range of lines is omitted, the operation is only performed on the current line. |
| s | Specifies the operation. In this case, substitution (search-and- replace). |
| /Line/line/ | The search pattern and the replacement text. |
| g | This means “global” in the sense that the search-and-replace is performed on every instance of the search string in the line. If omitted, only the first instance of the search string on each line is replaced. |


To specify a substitution command with user confirmation, adding a “c” to the end of the command.

```
:%s/Line/line/gc
```

Then vi stops and asks us to confirm the substitution with this message:

```
replace with Line (y/n/a/q/l/^E/^Y)?
```

what is the meaning of each key?

| Key | Action |
| --- | ------ |
| y | Perform the substitution. |
| n | Skip this instance of the pattern. |
| a | Perform the substitution on this and all subsequent instances of the pattern. |
| q or Esc | Quit substituting |
| l | Perform this substitution and then quit. Short for “last.” |
| Ctrl-e, Ctrl-y | Scroll down and scroll up, respectively. Useful for viewing the context of the proposed substitution. |


### Editing Multiple Files

```
vi file1 file2 file3....
```

#### Switching Between Files

To switch from one file to the next use:

```
:n
```

To move back to the previous file use:

```
:N
```

- While we can move from one file to another, vi enforces a policy that prevents us from switching files if the current file has unsaved changes. To force vi to switch files and abandon your changes, add an exclamation point (!) to the command.

To view a list of files being edited use:

```
:buffers
```

To switch to another buffer (file), type `:buffer` followed by the number of the buffer you wish to edit.for example,

```
:buffer 2
```

screen now displays the second file.

#### Opening Additional Files For Editing

The ex command :e (short for “edit”) followed by a filename will open an additional file.

```
:e lab.bak
```
to verify use:
```
:buffers
```

Note:

 - You cannot switch to files loaded with the `:e` command using either the `:n` or `:N` command.

 - To switch files, use the `:buffer` command followed by the buffer number.

#### Copying Content From One File Into Another
An example.

```
:buffer 1
```

type yy to copy a line.

```
:buffer 2
```

type p

#### Inserting An Entire File Into Another

```
:r foo.txt
```
The :r command (short for “read”) inserts the specified file before the cursor position in a file.

### Saving Work

- In command mode, typing ZZ will save the current file and exit vi.

- :wq will also save the current file and exit vi.

The :w command may also specify an optional filename. This acts like “Save As...”.

```
:w  foo1.txt
```

Note :

While the command above saves the file under a new name, it does not change the name of the file you are editing. As you continue to edit, you will still be editing foo.txt, not foo1.txt.

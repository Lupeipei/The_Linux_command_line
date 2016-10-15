# Redirection

### Standard Input, Output, And Error
programs such as ls actually send their results to a special file called **standard output (often expressed as stdout)** and their status messages to another file called **standard error (stderr).**

Note: **By default, both standard output and standard error are linked to the screen and not saved into a disk file.**

### Redirecting Standard Output
using the `>` redirection operator followed by the name of the file.
```
ls -l /var/log/syslog > ls-log.txt
```
+ when we redirect output with the `>` redirection operator, the destination file is always **rewritten** from the beginning.

+ You can create a new, empty file like this:`> ls-log.txt`

Using the `>>` operator will result in the output being appended to the file.

```
ls -l /usr/bin >> ls-log.txt
```

### Redirecting Standard Error

+ A program can produce output on any of several numbered file streams.

+ While we have referred to the first three of these file streams as standard input, output and error, the shell references them internally as file descriptors 0, 1 and 2, respectively.

#### Redirecting Standard Error To One File
    ```
    ls -l /bin/usr 2> ls-error.txt
    ```
#### Redirecting Standard Output and Standard Error To One File
+ traditional way :
    ```
    ls -l /bin/usr > ls-data.txt 2>&1
    ```

+ more streamlined way :
    ```
    ls -l /bin/usr &> ls-data.txt
    ```

You may also append the standard output and standard error streams to a single file.
    ```
    ls -l /bin/usr &>> ls-data.txt
    ```
#### Disposing Of Unwanted Output
Sometimes, we don't want output from a command, we just want to throw it away.
There is a special file called **“/dev/null”** which is a system device called a *bit bucket* which accepts input and does nothing with it.

```
ls -l /bin/usr 2> /dev/null
```

### Redirecting Standard Input

- `cat` is often used to display short text files.
```
cat ls-data.txt
```

- `cat` can also be used to join files together.
```
cat movie.mpeg.0* > movie.mpeg
```
- `cat` with no arguments is the way for stdin.
```
cat
```
press **Ctrl-d** to tell `cat` that it has reached end of file (EOF) on standard input.

- `cat >`: to create a file.
```
cat > hello.txt
hello word
```

- `cat <` : change the source of standard input from the keyboard to the file.
```
cat < hello.txt
```


### Pipelines

The ability of commands to read data from standard input and send to standard output is utilized by a shell feature called **pipelines**. Using "|".
```
command1 | command2
```
Say you want to examine the output of any command that produces standard output conveniently, using :
```
ls -l /usr/bin |less
```

**The Difference Between > and | :**

`>` connects a command with a file while `|` connects the output of one command with the input of a second command.

**Be careful!**
- The redirection operator silently creates or overwrites files, so you need to treat it with a lot of respect :)

#### Filters
```
ls /bin/usr /bin | sort | less
```
Since we specified two directories (/bin and /usr/bin), the output of ls would have consisted of two sorted lists, one for each directory. By including `sort` in pipeline, we changed the data to produce a single, sorted list.

#### uniq - Report Or Omit Repeated Lines
+ `uniq` is used to remove any duplicates from the output of the sort command.
    ```
    ls /bin /usr/bin | sort | uniq | less
    ```
+  Add `-d` option to `uniq` to see the duplicates.
    ```
    ls /bin /usr/bin | sort | uniq -d | less
    ```

#### wc – Print Line, Word, And Byte Counts
+ `wc` is used to display the number of **lines, words, and bytes** contained in files.
```
wc ls-data.txt
```
+ The `wc -l` limits its output to only report **lines**.
```
ls /bin /usr/bin | sort | uniq | less | wc -l
```

#### grep – Print Lines Matching A Pattern

```
grep pattern [file....]
```

for example:
```
ls /bin /usr/bin | sort | uniq | grep  zip
```
options for `grep`:
+ “-i” which causes grep to ignore case when performing the search (normally searches are case sensitive).

+ “-v” which tells grep to only print lines that do not match the pattern.

#### head / tail – Print First / Last Part Of Files
+ The `head` command prints **the first ten lines of a file** by default.

+ The `tail` command prints **the last ten lines** by default.

+ Both can be adjusted with the “-n” option.

+ `tail -f` allows you to view files in real-time.

    ```
    head -n 5 ls-data.txt
    tail -n 5 ls-data.txt
    ls /usr/bin | tail -n 5
    tail -f /var/log/syslog
    ```

Using the “-f” option, `tail` continues to monitor the file and when new lines are appended, they immediately appear on the display. This continues until you press **Ctrl-c**.

#### tee – Read From Stdin And Output To Stdout And Files
+ The `tee` program reads standard input and copies it to both standard output (allowing the data to continue down the pipeline) and to one or more files.

+ This is useful for capturing a pipeline's contents at an intermediate stage of processing.

an example:
```
ls /usr/bin | tee ls.txt | grep zip
```


### Linux is about imagination. It does what you want.

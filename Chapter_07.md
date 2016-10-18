# Seeing the world as the shell sees it

### Expansion
- Each time we type a command and press the enter key, bash performs several processes upon the text before it carries out our command.

- The process that makes this happen is called expansion.

An example :
```
echo *
```
The shell expands the “\*” into something else (in this instance, the names of the files in the current working directory) before the echo command is executed.

#### Pathname Expansion

The mechanism by which wildcards work is called *pathname expansion*.
```
echo D*
output: Desktop Documents
echo *s
output: Documents Pictures Templates Videos
```

Note:`echo *` does not reveal hidden files.
To show hidden files :
```
echo .[!.]*
```

#### Tilde Expansion(~)

It expands into the name of the home directory of the named user, or if no user is named, the home directory of the current user:
```
echo ~
```

#### Arithmetic Expansion
form:
```
$((expression))
```
- Expression is an arithmetic expression consisting of values and arithmetic operators.(+,-,\*,/,%,\*\*)

- Arithmetic expansion only supports integers.

```
echo $(((5**2)*3))
output: 75
```

#### Brace Expansion({})
```
echo F{A,B,C}-
output: FA- FB- FC-
```

```
echo {01..15}
output:01 02 03 04 05 06 07 08 09 10 11 12 13 14 15
```

```
echo a{A{1,2},C{1,2}}
output: aA1 aA2 aC1 aC2
```

 Note: The most common application is to make lists of files or directories to be created.
 ```
 mkdir {2007..2009}-{01..12}

 output:
 2007-01 2007-07 2008-01 2008-07 2009-01 2009-07 2007-02 2007-08 2008-02 2008-08 2009-02 2009-08 2007-03 2007-09 2008-03 2008-09 2009-03 2009-09 2007-04 2007-10 2008-04 2008-10 2009-04 2009-10 2007-05 2007-11 2008-05 2008-11 2009-05 2009-11 2007-06 2007-12 2008-06 2008-12 2009-06 2009-12
 ```

#### Parameter Expansion

- It's a feature that is more useful in shell scripts than directly on the command line.

- Many of its capabilities have to do with the system's ability to store small chunks of data and to give each chunk a name.

- Many such chunks, more properly called variables, are available for your examination.

- With parameter expansion, if you misspell the name of a variable, the expansion will still take place, but will result in an empty string.

```
echo $USER
```

#### Command Substitution

Command substitution allows us to use the output of a command as an expansion.

```
ls -l $(which cp)
ls -l `which cp`
file $(ls -d /usr/bin/* | grep zip)
```

### Quoting

#### Double Quotes

If we place text inside double quotes, all the special characters used by the shell **lose their special meaning and are treated as ordinary characters.** The exceptions are **“$”, “\\” (backslash), and “\`” (back- quote)**.

Remember, **parameter expansion, arithmetic expansion, and command substitution** still take place within double quotes.

```
echo this is a   test
output: this is a test

echo "this is a   test"
output: this is a   test

echo "$USRE $((2+2))"
output: me 4
```

The fact that newlines are considered delimiters by the word-splitting mechanism causes an interesting, albeit subtle, effect on command substitution.

```
echo $(cal)
October 2016 Su Mo Tu We Th Fr Sa 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31

echo "$(cal)"
October 2016
Su Mo Tu We Th Fr Sa
               1
2  3  4  5  6  7  8
9 10 11 12 13 14 15
16 17 18 19 20 21 22
23 24 25 26 27 28 29
30 31

```

#### Single Quotes

suppress all expansions.

```
echo 'text ~/*.txt {a,b} $(echo foo) $((2+2)) $USER'

text ~/*.txt {a,b} $(echo foo) $((2+2)) $USER
```

#### Escaping Characters
using `\`.

  To allow a backslash character to appear, escape it by typing “\\\”.

the backslash is also used as part of a notation to represent certain special characters called *control codes*.


| Escape Sequence | Meaning |
| --------------- | ------- |
| \a | Bell (“Alert” - causes the computer to beep) |
| \b | Backspace |
| \n | Newline. On Unix-like systems, this produces a linefeed. |
| \r | Carriage return |
| \t | Tab |

Adding the “-e” option to `echo` will enable interpretation of escape sequences. You may also place them inside $' '.
An example:
```
sleep 10; echo -e "Time's up\a"
```
also do this:
```
sleep 10; echo "Time's up" $'\a'
```

# Processes

### How A Process Works
- When a system starts up, the kernel initiates a few of its own activities as processes and launches a program called **init**.

- init, in turn, runs a series of shell scripts (located in /etc) called *init scripts*, which start all the system services.

- Many of these services are implemented as **daemon programs**, programs that just sit in the background and do their thing without having any user interface. So even if we are not logged in, the system is at least a little busy performing routine stuff.

- The kernel maintains information about each process to help keep things organized.

- Each process is assigned a number called a process ID or PID.

- PIDs are assigned in ascending order, with init always getting PID 1.

- The kernel also keeps track of the memory assigned to each process, as well as the processes' readiness to resume execution.

### Viewing Processes

```
ps
output :
PID TTY           TIME CMD
467 ttys000    0:00.03 -bash
```

- *TTY* is short for “Teletype,” and refers to the controlling terminal for the process.

- The *TIME* field is the amount of CPU time consumed by the process.

`ps x` to show all of our processes regardless of what terminal (if any) they are controlled by.


```
ps x
output :
PID   TT  STAT      TIME COMMAND
292   ??  S      0:00.72 /usr/libexec/UserEventAgent (Aqua)
294   ??  S      0:00.65 /usr/sbin/distnoted agent
296   ??  S      0:01.26 /usr/sbin/cfprefsd agent
297   ??  S      0:00.86 /System/Library/Frameworks/CoreTelephony.framework/S
298   ??  S      0:00.32 /usr/libexec/lsd
.....
```
- The presence of a “?” in the TTY column indicates no controlling terminal.

- STAT is short for “state” and reveals the current status of the process:

| State | Meaning |
| ----- | ------- |
| R | Running. This means that the process is running or ready to run. |
| S | Sleeping. The process is not running; rather, it is waiting for an event, such as a keystroke or network packet. |
| D | Uninterruptible Sleep. Process is waiting for I/O such as a disk drive. |
| T | Stopped. Process has been instructed to stop. More on this later. |
| Z | A defunct or “zombie” process. This is a child process that has terminated, but has not been cleaned up by its parent. |
| < | A high priority process. It's possible to grant more importance to a process, giving it more time on the CPU. This property of a process is called niceness. A process with high priority is said to be less nice because it's taking more of the CPU's time, which leaves less for everybody else. |
| N | A low priority process. A process with low priority (a “nice” process) will only get processor time after other processes with higher priority have been serviced. |

Another popular set of options is “aux” (without a leading dash):

```
ps aux
output :
USER              PID  %CPU %MEM      VSZ    RSS   TT  STAT STARTED      TIME COMMAND
_coreaudiod       218   2.4  0.1  2474332   8380   ??  Ss    9:35AM   0:54.00 /
lucia             559   1.7 14.4  3815500 1207692   ??  S     9:41AM   3:20.95 /
lucia             461   1.4  2.8  4196848 235416   ??  S     9:36AM   1:27.31 /
_hidd             108   0.8  0.1  2473508   5468   ??  Ss    9:35AM   0:41.37 /
_windowserver     154   0.6  1.2  3719428 104684   ??  Ss    9:35AM   1:05.90 /
lucia             463   0.4  0.4  2602308  32428   ??  S     9:36AM   0:04.70 /
lucia             556   0.1  0.1  2467240   5996   ??  S     9:41AM   0:07.06 /
.....
```

**Using the options without the leading dash invokes the command with “BSD style” behavior.**

BSD Style ps Column Headers:

| Header | Meaning |
| ------ | ------- |
| USER | User ID. This is the owner of the process. |
| %CPU | CPU usage in percent. |
| %MEM | Memory usage in percent. |
| VSZ | Virtual memory size. |
| RSS | RSS Resident Set Size. The amount of physical memory (RAM) the process is using in kilobytes. |
| START | Time when the process started. For values over 24 hours, a date is used. |

#### Viewing Processes Dynamically With top

```
top
```

### Controlling Processes

take *xlogo* as an example.

#### Interrupting A Process

In a terminal, pressing **Ctrl-c**, interrupts a program.

Many (but not all) command-line programs can be interrupted by using this technique.

#### Putting A Process In The Background

```
xlogo &

output: [1] 28236
```
output is consist of a job control and PID.

The shell's job control facility also gives us a way to list the jobs that have been launched from our terminal.
```
jobs
```

#### Returning A Process To The Foreground

The command `fg` followed by a percent sign and the job number (called a jobspec) :

```
fg %1
```

- As with the `fg` command, the jobspec is optional if there is only one job.

- To terminate xlogo, press Ctrl-c.

#### Stopping (Pausing) A Process

To stop a foreground process, press Ctrl-z.

Moving a process from the foreground to the background is handy if we launch a graphical program from the command, but forget to place it in the background by appending the trailing “&”.

### Signals

The kill command is used to “kill” processes.

- The kill command doesn't exactly “kill” processes, rather it sends them signals.

#### Sending Signals To Processes With kill

```
kill [-signal] PID
```
**common signals**:

| Number | Name | Meaning |
| ------ | ---- | ------- |
| 1 | HUP | Hangup. The signal is used to indicate to programs that the controlling terminal has “hung up.” |
| 2 | INT | Interrupt. Performs the same function as the Ctrl-c key sent from the terminal. It will usually terminate a program. |
| 9 | KILL | Kill. This signal is special. Whereas programs may choose to handle signals sent to them in different ways, including ignoring them all together, the KILL signal is never actually sent to the target program. Rather, the kernel immediately terminates the process.  |
| 15 | TERM | Terminate. This is the default signal sent by the kill command. If a program is still “alive” enough to receive signals, it will terminate. |
| 18 | CONT | Continue. This will restore a process after a STOP signal. |
| 19 | STOP | Stop. This signal causes a process to pause without terminating. Like the KILL signal, it is not sent to the target process, and thus it cannot be ignored. |

Examples:
```
kill -INT 2325
kill -1 2321
kill -SIGINT 2325
```

A complete list of signals can be seen with the following command:
```
kill -l
```

#### Sending Signals To Multiple Processes With killall

```
killall [-u user][-signal] name...
```

an example:
```
killall xlogo
```

### Shutting Down The System

There are four commands that can perform this function : `halt`, `poweroff`, `reboot`, and `shutdown`.

The first three are pretty self-explanatory and are generally used without any command line options.

```
sudo reboot
sudo halt
sudo poweroff
```

With `shutdown`, you can specify which of the actions to perform (halt, power down, or reboot), and provide a time delay to the shutdown event.

```
sudo shutdown -h now
sudo shutdown -r now
```

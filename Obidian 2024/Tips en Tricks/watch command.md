#linux 

## Linux Watch Command Syntax

The **`watch`** command uses the following syntax:

```
watch [option] [command]
```

Where:

- **`[option]`**: Adding an option changes the way the **`watch`** command behaves. Available options are listed below.
- **`[command]`**: A user-defined command you want to run repeatedly.

The **`watch`** command options include:

|   |   |
|---|---|
|**`-n`, `--interval`**|Allows you to specify the interval between output updates.|
|**`-d`, `--differences`**|Highlights the differences between output updates.|
|**`-g`, `--chgexit`**|Exits the **`watch`** command when the output of the user-defined command changes.|
|**`-t`, `--no-title`**|Removes the header showing the interval, command, and current time and date.|
|**`-b`, `--beep`**|Plays a sound alert (beep) if the command exits with an error.|
|**`-p`, `--precise`**|Attempts to run the command after the exact number of seconds defined by the **`--interval`** option.|
|**`-e`, `--errexit`**|Stops output updates on error and exits the command after a key press.|
|**`-c`, `--color`**|Interprets ANSI color and style sequences.|
|**`-x`, `--exec`**|Passes the user-defined command to **`exec`**, reducing the need for extra quoting.|
|**`-w`, `--no-linewrap`**|Turns off line wrapping and truncates long lines instead.|
|**`-h`, `--help`**|Displays help text and exits.|
|**`-v`, `--version`**|Displays version information and exits.|

## Linux Watch Command Examples

Here are some of the ways you can use the **`watch`** command options to achieve different results:

### Run Command with a Custom Interval

Set a custom interval to run a user-defined command and show the output by using the **`-n`** or **`--interval`** option:

```
watch -n [interval in seconds] [command]
```

For instance, to display the system time and date every 5 seconds, run:

```
watch -n 5 date
```

![Use the -n option to set a custom interval](https://phoenixnap.com/kb/wp-content/uploads/2021/08/linux-watch-command-01-custom-interval.png)

**Note:** The **`-n`** option allows you to use fractions of a second, with a minimum interval of 0.1 seconds. When entering decimals, both a period (**.**) and a comma (**,**) work for any locale.

### Highlighting Changes Between Updates

Use the **`-d`** or **`--difference`** option to highlight changes between successive output updates:

```
watch -d [command]
```

For example, display the system date and time in the default 2-second interval with the changes highlighted:

```
watch -d date
```

![Use the -d option to highlight changes between outputs](https://phoenixnap.com/kb/wp-content/uploads/2021/08/linux-watch-command-02-track-differences.png)

Pass **`=cumulative`** to the **`-d`** option if you want all the values that have ever changed to stay highlighted:

```
watch -d=cumulative date
```

### Exit on Change

The **`-g`** or **`--chgexit`** option causes the watch command to exit if there is a change in the output:

```
watch -g [command]
```

As an example, adding the [free command](https://phoenixnap.com/kb/free-linux-command) monitors your system's memory consumption and exits if the value changes:

```
watch -g free
```

![Use the -g option to exit the watch command if the output changes](https://phoenixnap.com/kb/wp-content/uploads/2021/08/linux-watch-command-03-exit-on-change.png)

### Hide the watch Command Header

Turn off the header containing the interval time, user-defined command, and current system time in the **`watch`** command output by using the **`-t`** or **`--no-title`** option:

```
watch -t [command]
```

Returning to the example of displaying the system date and time, this time without the header:

```
watch -t date
```

![Use the -t option to display the watch command output without the header](https://phoenixnap.com/kb/wp-content/uploads/2021/08/linux-watch-command-04-no-header.png)

### Alert on Error

The **`watch`** command uses the beep package to play a sound alert if the output update fails due to an error. To do this, use the **`-b`** or **`--beep`** option:

```
watch -b [command]
```

**Note:** if you don't have the beep package installed, add it with **`sudo apt install beep`** command.

### Using Complex Commands

The **`watch`** command also allows you to use more complex user-defined commands, with their own arguments and options. One way to do this is to use the backslash (**'\'**) symbol:

```
watch [options] \
```

Using the command above brings you to the next line in the terminal, where you need to add the user-defined command. Once you hit **Enter**, it executes the command. For instance:

```
watch -n 5 \
echo "watch command example output"
```

![Adding a complex command using the backslash symbol](https://phoenixnap.com/kb/wp-content/uploads/2021/08/linux-watch-command-05-complex-command-backslash.png)

Another option is to add the user-define command in single quotation marks:

```
watch [options] '[command]'
```

Using the example above, the command would be:

```
watch -n 5 'echo "watch command example output"'
```

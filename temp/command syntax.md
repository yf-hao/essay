## entering more than  one command at a time

```bash
date; cal
```

## what happens when you enter a command

for example:
```bash
ls -l -F file1
```

When you press the <Return> key, the shell processes a command line by assuming that the first part of the line is the name of a command you want to run. The shell then searches for and executes the program by that name. 
When the shell does find the program you want, it runs it. At that time. the shell sends a copy of the entire command line to the program. It is up to the program to figure out what to do with all the information.

## command syntax

```bash
command-name options arguments
```
- options : control how a command should do its job
- arguments: specify the data you want the command to use
  
### options


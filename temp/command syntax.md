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

As the name implies, the use of options is optional.

An option consitsts of either a hyphen followed by a single letter, or two hyphens followed by  a word.
```bash
ls -l  
ls --help
```
### arguments

Arguments are used on the command line to pass information  to the poragram you want to run.

## The formal description of a command : syntax

A good approach to learing a new command is to answer the following three questions:
- what does the command do?
- How do I use the options?
  - one hyphen followed by a single letter
  - two hyphens followed by a word
- How do I use the arguments?
  - one or more
  - zero or more

within Unix, command sytax follows seven rules:
1. Items in square brackets are optional
2. Itmes not in square brackets are obligatory.
3. Anything in boldface must be typed exactly as written
4. Anything in italics must be replaced by an appropriate  value
5. An grgument followed by an ellipsis(...) may be repeated any number of times

![](https://raw.githubusercontent.com/fray-hao/images/master/20190327154904.png)


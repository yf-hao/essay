
### Definition
The manual is a collection of files, each of which contains doucumentation about one specific Unix command or topic.
### shortkey
![](https://raw.githubusercontent.com/fray-hao/images/master/20190320142736.png)

### section
![](https://raw.githubusercontent.com/fray-hao/images/master/20190321074843.png)

Example:
```bash
man 2 kill 
```

![](https://raw.githubusercontent.com/fray-hao/images/master/20190321075108.png)

###  reference
![](https://raw.githubusercontent.com/fray-hao/images/master/20190321075421.png)

As you can see, The first reference is in section 1. Three of the references are in section 2. The last reference is in section 8
```bash
man 2 stat
```
###  The format of a manual page
![](https://raw.githubusercontent.com/fray-hao/images/master/20190321080855.png)

- Synopsis
  In general, when you enter a command, you type a name,followed by options,followed by parameters.

  There are two variations of how the Synopsis section shows the options

  Frist, you may simply see the word Option. In this case, the actual options are listed and explained in the Description section below.
    ```bash
    ls [OPTION]... [FILE]...
    ```
  This convention is used with the man pages that come with the GNU utilities.
  
  In the second case, the actual options are specified.
  ```bash
    ls [-ABCFGHLPRTWabcdfghiklmnopqrstuwx1] [file...]
  ```  
###  A quick way to find out what a command does

```bash
man -f time
```
As a convenience，you can use the command whatis as a synonym for man -f：
```bash
whatis time
```
### searching for a command

```bash
man -k printf
```
search the short descriptions and manual page names for the keyword printf as regular expression. print out any matches

as a convenience， you can use the single word apropos as a synonym for man -k:
```bash
apropos printf
```
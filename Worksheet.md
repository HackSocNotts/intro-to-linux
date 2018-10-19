# Intro to Linux

### What we'll cover

- What is Linux?
- Basic commands and traversing the file system
- File manipulation
- Pipes and redirection
- System administration
- Debian package manager (`apt`)

### Getting started

**If you're on a Windows machine:**

- You'll need to install [PuTTY](https://the.earth.li/~sgtatham/putty/latest/w64/putty-64bit-0.70-installer.msi). The lab computers already have this installed, so you only need to do this if you're using your own laptop.
- Once you've got that installed, open it and type `ubuntu01.cloud.hacksoc.net` into the "Host Name or IP Address" box and press Open.
- You'll be prompted for a username and password, so enter them into the window. Note that as you type your password, nothing will appear, but it's still working.

**If you're on a Mac or Linux computer:**

- Open a Terminal window. If you're on a Mac, you can do this by pressing Command + Space, and typing "Terminal" into the search box that appears.
- You can then use the `ssh` command to log into the servers.
- In your Terminal window, type `ssh user-[number]@ubuntu01.cloud.hacksoc.net` followed by enter - for example, if your username was `user-65`, the command would be `user-65@ubuntu01.cloud.hacksoc.net`.
- You'll be prompted for the password - as you type this, nothing will appear, but it's still working.

If you need any help with this, then feel free to ask one of our mentors for help!

### What is Linux?

The term 'Linux' refers to the 'kernel' that the system is running. The kernel has control over the whole system, and connects the application software on a computer to the CPU, memory and input/output devices. There are [literally hundreds](https://en.wikipedia.org/wiki/List_of_Linux_distributions) of linux distributions, and many more instances of linux running on embedded devices like in-flight entertainment systems, digital billboards, and other such things. The ethos behind the Linux ecosystem is having a 'free and open source' codebase, which means that the source code is public, and anybody is free to change it and re-release it (Under a different name). 

### Basic commands and traversing file systems

In Linux, everything is stored on the "file system" - a big tree of files and folders (called directories) where all of the user's files go, where all of the computer's settings are stored, et cetera. `/` is the "root" of the file system; everything in the file system is contained within this root directory.

There are a number of commands for helping you move around this file system. When you first log in, your working directory will be your user's home folder - users in Linux can have their own directory that they own & where they store their files. A shortcut for your home directory is the `~` symbol - if you see this, it means "home directory". The _working directory_ is the current location where any commands you run will take effect - for example, if you create a new directory, it will appear in your working directory.

You can find out what your working directory is by typing the `pwd` command. This will print a single line of output, which should look something like this:

```
/home/user-03
```

If you want to see a list of the files in your current working directory, you can use the `ls` command. This won't do anything, because your user directory is empty by default - we'll change that in the next section. For now, we can have a look to see what's in that root directory we mentioned earlier, by using `ls /`. This will give us a bunch of output, looking something like this:

![Image showing the output of ls /](https://i.imgur.com/E0lSdYR.png)

You can change your current working directory by using the `cd` command, followed by the directory you want to change to. For example, if you wanted to change your current working directory to `/`, you can do that by typing `cd /`. You can go back to your home directory by typing `cd ~` - you'll want to do this for the next section. You can also move up a directory by typing `cd ..`. Note that filenames in Linux are case-sensitive; you'll need to type them exactly as you see on your screen.
### File manipulation

**Before starting, make sure you're in the home directory: `cd ~`**

There are a number of commands in Linux that you can use to manipulate files and the file system, allowing you to create, edit and delete files at will.

The first command we'll look at is the `mkdir` command - this is shorthand for "make directory", and allows you to create directories. As an example of how to do this, let's make a directory with your name. Your command might look like this:

```
mkdir Toby
```

This will make a directory called "Toby" in the current working directory. You can then `cd` into it as discussed before: `cd Toby`.

Another command you can use is `touch`. This creates an empty file with the name you've specified. Let's create an empty file called `about-us`, in the folder we created before:

```
touch about-me
```

If you type `ls` now, you should see this in the list of files.

You can edit the file using `nano` - this is a simple command-line text editor built into most Linux machines. In this case, we'd type `nano about-me` to open this in `nano`. This will bring up a text editor - feel free to type some stuff about yourself in here.

Once you're done, press `Control` and `X` on your keyboard, press `Y` for Yes, and press Enter to save the file. You'll be returned to the 
command prompt.

You can view the contents of a file by using the `cat` command:

```
cat about-me
```

This will display the contents of the file in the terminal.

You can also move and copy files using the `mv` and `cp` commands:

```
mv [source] [destination]
cp [source] [destination]
```

For example, typing `mv about-me ~` will move the file `about-me` to your home directory. For now, let's go back to our home directory: `cd ~`

Finally, you can delete files and directories using the `rm` command. If you want to delete a file, just use `rm` on its own:

`rm about-me`

If you want to delete a directory, you need to add the `-r` flag to `rm` (which means _recursive_ - a fancy way of saying "delete this folder and everything inside of it"):

`rm -r Toby`

You can also download files using the `wget` command - let's use this to _literally download the entire works of Shakespeare_:

```
wget https://ocw.mit.edu/ans7870/6/6.006/s08/lecturenotes/files/t8.shakespeare.txt -O shakespeare.txt
```

This downloads the file in the link, and the -O option tells `wget` to save the file as "shakespeare.txt" in the current working directory. We'll use this later.

### Pipes and redirection

**Before starting, make sure you're in the home directory: `cd ~`**

It's important to know what standard streams are in Linux, as we'll be manipulating them later. Standard streams can be thought of as "pipes" - Linux can connect them to a program, and that program can read and write data to them. There's a couple of important ones that are useful in the context of this session:

- Standard output (also known as `stdout`): this is used for programs to output text to the screen.
- Standard input (also known as `stdin`): this is used for programs to read text that the user types in.

You can redirect these streams to other programs; for example, you can take the output of `cat`, and redirect it to another program.

One program that is useful for this is `grep` - this allows us to search for text inside files. For example, we can use the `grep` command to find all the instances of "Hamlet" inside the Shakespeare file:

```
cat shakespeare.txt | grep "Hamlet"
```

The `|` symbol _pipes_ the **output** of the `cat` command to the **input** of the `grep` command, which searches for all lines of text containing "Hamlet" on its input.

You can also chain these together. For example, we can add the `wc` command on the end - this allows us to see how many lines in the file contain the word Hamlet. That command would look like this:

```
cat shakespeare.txt | grep "Hamlet" | wc -l
```

This takes the **output** of `grep` and _pipes_ it to the **input** of the `wc` command.

### System administration

There are many tools you can use in Linux to keep on top of your computer, as well as some useful shortcuts and tricks. 

- `Ctrl + C` is a keyboard interrupt, and stops whatever process is being run on your terminal window. 
- Adding `&` to the end of a command in a terminal will make it run in the background, letting you do other things while it's running. (You can also use `command1 && command2` if you want to run two commands one after the other). 
- Copying and pasting in terminal windows uses `Ctrl + Shift + C/V` rather than just `Ctrl + C/V`. 
- `clear` will clear the terminal window of all previous text. 
- You can use the Tab key for the terminal to attempt to autocomplete your command or the directory you want to move to.

A helpful tool for commands you aren't familiar with is `man` - these are "manual pages" (also referred to as manpages), and they provide explanation of the commands in Linux and all of the different things you can do with them. Once you're looking at a manpage, you can use the arrow keys on your keyboard to scroll through the document, and press the `Q` key on your keyboard to exit. A large number of commands also offer the `command --help` option, which gives a less detailed but helpful nonetheless output.

`top` is a command that provides your terminal interface with a constantly updating list of programs, organised from most demanding to least demanding, along with providing a summary of various system facts. It will tell you: 
The time, the system uptime, how many users are logged in (Try the `who` command to see who is currently logged onto the system), the amount of tasks and whether they're running, idle or otherwise; It will also give you a listed breakdown of the processes that are using the most CPU power which can be helpful for identifying troublesome programs that are slowing down your system. You can press `Shift + F` to sort by lots of different metrics like RAM usage, uptime and so on, then select a metric, press enter, and then escape. You can exit the program by pressing 'Q' 

Another tool that's useful is `ps` - this is a tool that shows us all of the running programs (called processes) on our computer. Typing `ps -e` will show all running programs on the computer in a list. You can also use `pstree` to show the process tree - processes in Linux can start other processes, and these are referred to as _child processes_. `pstree` will show all processes and their children in a tree diagram.

You can use the `kill` command to stop programs from running - use this carefully, as you can cause your computer to crash by killing the wrong process. You'll notice that the output of `ps` contains a list of numbers; these are called _process IDs_. You can give these to `kill` to specify which process you want to kill. For example, typing `kill 9374` will kill the process with the ID for 9374. Sometimes `killall (process)` is more helpful, as it can kill all of a program's subprocesses as well. `killall firefox` will terminate all of its processes, for example.

If you're not sure which user account you're logged in as, you can use `whoami` to find out. Typing this on its own will tell you which user you're currently logged in as.

In Linux, there is a default user called `root` which has permission to make any changes it wants to the system. If you want to run a command as `root`, you can use the `sudo` command, followed by the command you wanted to run anyway. For example, the `apt-get` command won't work if you're logged in as a standard user; you'd need to put `sudo` in front of your command to make it work:

```
sudo apt-get [...]
```
Note: Be careful when using `sudo` or `su`, as with great power comes great responsibility. Make sure you understand what you're typing into the terminal as you can introduce security vulnerabilities or break your entire system.

You can also use the `which` command to find the location of any program installed in your system - for example, typing `which ls` will tell you where `ls` is installed on your computer.

### Debian package manager (`apt`)

**Make sure you use `sudo` as explained in the previous section if you receive permissions errors.**

Firstly, it's important to know what a Linux distribution is and what it means. A distribution is a "flavour" of Linux tailored to a particular purpose - they are also often referred to as "distros". A popular Linux distro exists called Debian - this is a very simple general purpose distribution, and lots of people base their distributions on top of this.

One popular feature of Debian is its package manager - this is called `apt`. Using `apt` (or `apt-get`), you can install new software (called packages) from the command line, handling the download and installation for you. `apt` fetches software from _repositories_ - these are effectively just Web sites filled with lists of software that your computer can use to look for the software you want. Debian distributions come with a set of default repositories, which is good enough for most people, but you can add more to expand the list of software you can install.

You use the `apt-get` command to install software - as an example, if you wanted to install the `tree` command on your computer, you would type `apt-get install tree`. This will automatically download and install the `tree` package for you.

If you want to search for a piece of software in the repositories, you can use the `apt-cache` command. For example, if I wanted the `elinks` command, but wasn't sure what the package name is, you can use `apt-cache search elinks`. This will give you a list of all the packages that match "elinks" - you can then install that package using `apt-get install`.

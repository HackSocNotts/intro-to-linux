# Intro to Linux

### What we'll cover

- A brief history of Linux
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

For example, typing `mv about-me ~` will move the file `about-me` to your home directory.



### Pipes and redirection

### System administration

### Debian package manager (`apt`)
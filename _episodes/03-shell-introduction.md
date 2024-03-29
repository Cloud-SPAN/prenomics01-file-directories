---
title: "Introducing the Shell"
teaching: 45
exercises: 15
questions:
- "What is a command shell and why would I use one?"
- "How can I move around on my computer?"
- "How can I see what files and directories I have?"
- "How can I specify the location of a file or directory on my computer?"
objectives:
- "Describe key reasons for learning shell."
- "Navigate your file system using the command line."
- "Access and read help files for `bash` programs and use help files to identify useful command options."
- "Demonstrate the use of tab completion, and explain its advantages."
- "Use a single command to navigate multiple steps in your directory structure, including moving backwards (one level up)."
- "Work with hidden directories and hidden files."
keypoints:
- "The shell gives you the ability to work more efficiently by using keyboard commands rather than a GUI."
- "Useful commands for navigating your file system include: `ls`, `pwd`, and `cd`."
- "Most commands take options (flags) which begin with a `-`."
- "Tab completion can reduce errors from mistyping and make work more efficient in the shell."
- "Hidden files and directories start with `.` and can be viewed using `ls -a`."
---

## What is a shell and why should I care?

A *shell* is a computer program that has a command line where you type commands to do 
things on your computer rather than using menus and buttons on a Graphical User Interface (GUI).

There are many reasons to learn about the shell:

* Many bioinformatics tools can only be used through a command line interface, or
have extra capabilities in the command line version that are not available in the GUI.
This is true, for example, of BLAST, which offers many advanced functions only accessible
to users who know how to use a shell.  
* In bioinformatics you often need to do the same set of tasks with a large number of files. A shell allows you to
automate such repetitive tasks.  
* The shell makes your work less error-prone. When humans do the same thing a many times
they make mistakes. Your computer can do the same thing a thousand times without mistakes.  
* The shell makes your work more reproducible. When you carry out your work in the command-line
(rather than a GUI), your computer keeps a record of every step that you've carried out, which you can use
to re-do your work when you need to. It also describes unambiguously what you've done,
so that others can check your work or apply your process to new data.  
* Many bioinformatic tasks require large amounts of computing power and can't realistically be run on your
own machine. These tasks are best performed using remote computers or cloud computing, which can only be accessed
through a shell.

In this lesson you will learn how to use the command line interface to move around in your file system.

## How to access the shell

We have already accessed the shell in the previous episode, when we logged onto the Cloud instance.

We will spend most of our time learning about the basics of the shell
by manipulating some experimental data. Some of the data we're going to be working with is quite large, and
we're also going to be using several bioinformatic packages in later
lessons to work with this data. To avoid having to spend time
downloading the data and downloading and installing all of the software,
we're going to continue using our Cloud instance.

As a reminder, we log in by launching Git Bash or Terminal from the `cloudspan` folder we made in today's first episode, and then using our `ssh` command.

~~~
$ ssh -i login-key-instanceNNN.pem  csuser@instanceNNN.cloud-span.aws.york.ac.uk
~~~
{: .bash}

After logging in, you will see a screen showing something like this:

~~~
Welcome to Ubuntu 20.04.3 LTS (GNU/Linux 5.4.0-84-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Thu 21 Oct 2021 10:47:55 AM UTC

  System load:  1.68               Processes:             189
  Usage of /:   24.0% of 98.30GB   Users logged in:       0
  Memory usage: 25%                IPv4 address for eth0: 10.0.32.254
  Swap usage:   0%

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

73 updates can be applied immediately.
32 of these updates are standard security updates.
To see these additional updates run: apt list --upgradable

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.
    _____________________________

    W E L C O M E    T O    T H E


     ____ _                 _         ______ _____   _    __   _
    / ___| | ___  _   _  __| |       / ____ |  _  \ / \  |  \ | |
   | |   | |/ _ \| | | |/ _` |  ___  \___  \| |_) '/ _ \ | \ \| |
   | |___| | (_) | |_| | (_| | |___| ____)  |  __ / ___ \| |\ | |
    \____|_|\___/ \___/ \__,_|       \_____/|_|  /_/   \_|_| \__|



    F O U N D A T I O N     C O U R S E     E N V I R O N M E N T

    _____________________________________________________________

    Scroll up with the mouse for information before this welcome

    Type "csguide" (and the Enter (↵) key) for some guidance
    _____________________________________________________________



Last login: Thu Oct 14 11:13:28 2021 from xxxxxxx
~~~
{: .output}

## Navigating your file system

Now we have logged into our Cloud instance, we have access to a new file directory. This instance has been set up with some existing files and directories for you, and we will also be adding some new ones later in the course.

Several commands are frequently used to create, inspect, rename, and delete files and directories.

~~~
$
~~~
{: .bash}

The dollar sign is a **prompt**, which shows us that the shell is waiting for input;
your shell may use a different character as a prompt and may add information before
the prompt. When typing commands, either from these lessons or from other sources,
do not type the prompt, only the commands that follow it.

Let's find out where we are by running a command called `pwd`
(which stands for "print working directory").
At any moment, our **current working directory**
is our current default directory,
i.e.,
the directory that the computer assumes we want to run commands in,
unless we explicitly specify something else.
Here,
the computer's response is `/home/csuser`,
which is the top level directory within our cloud system:

~~~
$ pwd
~~~
{: .bash}

~~~
/home/csuser
~~~
{: .output}

This `csuser` directory is our **home directory**.

Let's look at how our file system is organised. We can see what files and subdirectories are in this directory by running `ls`,
which stands for "listing":

~~~
$ ls
~~~
{: .bash}

~~~
bin  shell_data  software
~~~
{: .output}

`ls` prints the names of the files and directories in the current directory in
alphabetical order,
arranged neatly into columns.
We'll be working within the `shell_data` subdirectory, and creating new subdirectories, throughout this workshop.  

The command to change locations in our file system is `cd`, followed by a
directory name to change our working directory.
`cd` stands for "change directory".

Let's say we want to navigate to the `shell_data` directory we saw above.  We can
use the following command to get there:

~~~
$ cd shell_data
~~~
{: .bash}

Let's look at what is in this directory:

~~~
$ ls
~~~
{: .bash}

~~~
sra_metadata  untrimmed_fastq
~~~
{: .output}

We can make the `ls` output easier to understand by using the **flag** `-F`,
which tells `ls` to add a trailing `/` to the names of directories:

~~~
$ ls -F
~~~
{: .bash}

~~~
sra_metadata/  untrimmed_fastq/
~~~
{: .output}

Anything with a `/` after it is a directory. Things with a `*` after them are programs. If
there are no decorations, it's a file.

`ls` has lots of other options. To find out what they are, we can type:

~~~
$ man ls
~~~
{: .bash}

`man` (short for manual) displays detailed documentation (also referred as man page or man file)
for `bash` commands. It is a powerful resource to explore `bash` commands, understand
their usage and flags. Some manual files are very long. You can scroll through the
file using your keyboard's down arrow or use the <kbd>Space</kbd> key to go forward one page
and the <kbd>b</kbd> key to go backwards one page. When you are done reading, hit <kbd>q</kbd>
to quit.

> ## Challenge
> Use the `-l` option for the `ls` command to display more information for each item
> in the directory. What is one piece of additional information this long format
> gives you that you don't see with the bare `ls` command?
>
> Share your answer on the forum.
>
> > ## Solution
> > ~~~
> > $ ls -l
> > ~~~
> > {: .bash}
> >
> > ~~~
> > total 8
> > drwxr-x--- 2 dcuser dcuser 4096 Jul 30  2015 sra_metadata
> > drwxr-xr-x 2 dcuser dcuser 4096 Nov 15  2017 untrimmed_fastq
> > ~~~
> > {: .output}
> >
> > The additional information given includes the name of the owner of the file,
> > when the file was last modified, and whether the current user has permission
> > to read and write to the file.
> >
> {: .solution}
{: .challenge}

No one can possibly learn all of these arguments - that's what the manual page
is for! It does take practice to get used to using and understanding the information in the manual. 
Often, you don't need to understand completely what it is saying to be able to guess what to try.

Let's go into the `untrimmed_fastq` directory and see what is in there.

~~~
$ cd untrimmed_fastq
$ ls -F
~~~
{: .bash}

~~~
SRR097977.fastq  SRR098026.fastq
~~~
{: .output}

This directory contains two files with `.fastq` extensions. FASTQ is a format
for storing information about sequencing reads and their quality.
We will be learning more about FASTQ files in a later lesson.

Learning to navigate a new file directory can be confusing at first. To help, here is a tree diagram showing what we have explored so far. Do not worry about the `sra_metadata ` and `.hidden` directories, as they are not important right now.

![A file hierarchy tree](../fig/blank_instance_file_tree.png){:width="400px"}

First we moved from our home directory at `csuser` into the `shell_data` directory, which is one level down. From there we opened up the `untrimmed_fastq` directory, which contains two `.fastq` files.

Typing `cd` after the prompt and pressing enter will always take you back to your home directory.

### Shortcut: Tab Completion

It is very easy to make mistakes typing our filenames and commands. Thankfully, "tab completion"
can help us! When you start typing out the name of a directory or file, then
hit the <kbd>Tab</kbd> key, the shell will try to fill in the rest of the
directory or file name.

Return to your home directory:

~~~
$ cd
~~~
{: .bash}

then enter:

~~~
$ cd she<tab>
~~~
{: .bash}

The shell will fill in the rest of the directory name for
`shell_data`.

Now change directories to `untrimmed_fastq` in `shell_data`

~~~
$ cd shell_data
$ cd untrimmed_fastq
~~~
{: .bash}

Using tab complete can be very helpful. However, it will only autocomplete
a file or directory name if you've typed enough characters to provide
a unique identifier for the file or directory you are trying to access.

For example, if we now try to list the files which names start with `SR`
by using tab complete:  

~~~
$ ls SR<tab>
~~~
{: .bash}

The shell auto-completes your command to `SRR09`, because all file names in
the directory begin with this prefix. When you hit
<kbd>Tab</kbd> again, the shell will list the possible choices.

~~~
$ ls SRR09<tab><tab>
~~~
{: .bash}

~~~
SRR097977.fastq  SRR098026.fastq
~~~
{: .output}

Tab completion can also fill in the names of programs, which can be useful if you
remember the beginning of a program name.

~~~
$ pw<tab><tab>
~~~
{: .bash}

~~~
pwck      pwconv    pwd       pwdx      pwunconv
~~~
{: .output}

Displays the name of every program that starts with `pw`.

> ## Tip
>
> You might find it useful to keep a note of the commands you learn in this course, so you can easily remember them in future. This will be faster than scrolling through the course each time you forget a command. While using the Cloud-SPAN AMI you can also type 'csguide' into the command prompt and hit enter for a text-based guide to the command line, including frequently used commands.
{: .callout}

## Moving around the file system

Now we're going to learn some additional commands for moving around
within our file system.

Use the commands we've learned so far to navigate to the `shell_data/untrimmed_fastq` directory:

~~~
$ cd
$ cd shell_data
$ cd untrimmed_fastq
~~~
{: .bash}

What if we want to move back up and out of this directory and to our top level
directory? Can we type `cd shell_data`? Try it and see what happens.

~~~
$ cd shell_data
~~~
{: .bash}

~~~
-bash: cd: shell_data: No such file or directory
~~~
{: .output}

Your computer looked for a directory or file called `shell_data` within the
directory you were already in. It didn't know you wanted to look at a directory level
above the one you were located in.

We have a special command to tell the computer to move us back or up one directory level.

~~~
$ cd ..
~~~
{: .bash}


Now we can use `pwd` to make sure that we are in the directory we intended to navigate
to, and `ls` to check that the contents of the directory are correct.

~~~
$ pwd
~~~
{: .bash}

~~~
/home/csuser/shell_data
~~~
{: .output}

~~~
$ ls
~~~
{: .bash}

~~~
sra_metadata  untrimmed_fastq
~~~
{: .output}

From this output, we can see that `..` did indeed take us back one level in our file system.

You can chain these together like so:

~~~
$ ls ../../
~~~
{: .bash}

prints the contents of the folder called `home`

> ## Finding hidden directories
>
> First navigate to the `shell_data` directory. There is a hidden directory within this directory.
> Explore the options for `ls` in the man page to find out how to see hidden directories. 
> List the contents of the directory and identify the name of the text file in that directory.
>
> Share your answer on the forum!
>
> Hint: hidden files and folders in Unix start with `.`, for example `.my_hidden_directory`
>
> > ## Solution
> >
> > First use the `man` command to look at the options for `ls`.
> > ~~~
> > $ man ls
> > ~~~
> > {: .bash}
> >
> > The `-a` option is short for `all` and says that it causes `ls` to "not ignore
> > entries starting with ." This is the option we want.
> >
> > ~~~
> > $ ls -a
> > ~~~
> > {: .bash}
> >
> > ~~~
> > .  ..  .hidden	sra_metadata  untrimmed_fastq
> > ~~~
> > {: .output}
> >
> > The name of the hidden directory is `.hidden`. We can navigate to that directory
> > using `cd`.
> >
> > ~~~
> > $ cd .hidden
> > ~~~
> > {: .bash}
> >
> > And then list the contents of the directory using `ls`.
> >
> > ~~~
> > $ ls
> > ~~~
> > {: .bash}
> >
> > ~~~
> > youfoundit.txt
> > ~~~
> > {: .output}
> >
> > The name of the text file is `youfoundit.txt`.
> {: .solution}
{: .challenge}

In most commands the flags can be combined together in no particular order to obtain the desired results/output.
~~~
$ ls -Fa
$ ls -laF
~~~

## Summary

We now know how to move around our file system using the command line.
This gives us an advantage over interacting with the file system through
a GUI as it allows us to work on a remote server, carry out the same set of operations
on a large number of files quickly, and opens up many opportunities for using
bioinformatic software that is only available in command line versions.

In the next few episodes, we'll be expanding on these skills and seeing how
using the command line shell enables us to make our workflow more efficient and reproducible.

For now, log off using the `exit` command: This will close the connection, and your terminal will go back to showing your local computer prompt, for example:

~~~
csuser@instanceNNN:~ $ exit
~~~
{: .bash}

This will close the connection, and your terminal will go back to showing your local computer prompt, for example:
~~~
logout
Connection to instanceNNN.cloud-span.aws.york.ac.uk closed.
username@machineid $
~~~
{: .output}

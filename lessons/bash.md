# Introduction to Bash (The Linux Command Line)

![](./img/dilbert-1486.strip.gif)

-   Who has used the command line at all before?  Does anyone remember DOS?
-   Who currently uses an application which requires the command line?
-   Who has used Linux before?

## Introduction
-   Explain how the shell relates to the keyboard, the screen, the operating system, and users' programs.
-   Explain when and why command-line interfaces should be used instead of graphical interfaces.

-   A shell is a program whose primary purpose is to read commands and run other programs.
-   The shell's main advantages are its high action-to-keystroke ratio, its support for automating repetitive tasks, and that it can be used to access networked machines.
-   The shell's main disadvantages are its primarily textual nature and how cryptic its commands and operation can be.

-   `echo`
-   `echo $SHELL`
-   `whoami`
-   `who`
-   `man`


## Files & Directories
-   Explain the similarities and differences between a file and a directory.
-   Translate an absolute path into a relative path and vice versa.
-   Construct absolute and relative paths that identify specific files and directories.
-   Explain the steps in the shell's read-run-print cycle.
-   Identify the actual command, flags, and filenames in a command-line call.
-   Demonstrate the use of tab completion, and explain its advantages.

-   The file system is responsible for managing information on the disk.
-   Information is stored in files, which are stored in directories (folders).
-   Directories can also store other directories, which forms a directory tree.
-   `/` on its own is the root directory of the whole filesystem.
-   A relative path specifies a location starting from the current location.
-   An absolute path specifies a location from the root of the filesystem.
-   Directory names in a path are separated with `/` on Unix, but `\` on Windows.
-   `..` means "the directory above the current one"; `.` on its own means "the current directory".
-   Most files' names are `something.extension`. The extension isn't required, and doesn't guarantee anything, but is normally used to indicate the type of data in the file.
-   Most commands take options (flags) which begin with a `-`.

Consider the file system below.  All of the directories are descended from the master
root directory `/`.  Each of the top-level directories descend directly from `/`
(and there are many other standard directories on Unix-derived systems:
`/bin`, `/mnt`, `/opt`, etc.).

![](./img/file-system-01.png)

Within any one of these folders we can identify a subsidiary structure:

![](./img/file-system-02.png)

And then we can drill down all the way to something that perhaps looks more
familiar to you, a home directory populated with files just like you may treat
the `My Documents` folder on Windows.

![](./img/file-system-03.png)

To navigate this system on the command line (as opposed to in a file browser),
you only need a few basic commands:

-   `ls` and its modifications show you what the file system looks like.
    -   `-l`, `-a`, `-t`, `-h`, `-r`, `-color=auto`
-   `cd`
-   `pwd`

Unix-like systems treat all devices as if they were files.  For instance, if
you were to list the contents of the `/media` directory, you may see attached
USB or network drives, if any.  `mount` tells you about which logical volumes
(disk drives) are attached to your computer now, and lets you attach new ones
if necessary (rarely needed explicitly on modern systems).
-   `mount`

By the way, there are a few handy shortcuts we have available for our
navigation and command-line work:
-   TAB auto-completion, ↑↓
-   `.`, `..` directories

### Exercises

![file-system](./img/file-system-exercise.png)

-   If `pwd` displays `/home/thesis`, what will `ls ../thesis` display?

-   If `pwd` displays `/home`, and `-r` tells `ls` to display things in
    reverse order, what command will display `refs/ main/ data/` ?

-   Similarly, if `pwd` displays `/thesis/main`, what command will display
    the same output as before?

-   What does the command `cd` without a directory name do?


## Create files and folders
-   Create a directory hierarchy that matches a given diagram.
-   Create files in that hierarchy using an editor or by copying and renaming existing files.
-   Display the contents of a directory using the command line.
-   Delete specified files and/or directories.

-   Unix documentation uses `^A` to mean "control-A".
-   The shell does not have a trash bin: once something is deleted, it's really gone.
-   Nano is a very simple text editor—please use something else for real work.

-   `cp`
-   `nano`
-   `vi`
-   `$PATH`
-   `mv`
-   `cd`
-   `$HOME`, `~`

### Wildcards

-   `*`
-   `?`
-   `{1-3}`

-   `touch`
    -   `touch file.out.1-3`
    -   `touch file.out.{1..3}`
    -   `ls *[1-3]*`
    -   `rm /a/long/path/foo /a/long/path/bar`
    -   `rm /a/long/path/{foo,bar}`

-   `mkdir`
-   `cp -r`
-   `cat`
-   `rm`, `rm -r`, `rm -r -f`
-   `echo rm *[AB].txt`---there is no recycle bin

### Advanced
-   `wget`
-   `tar -xvzf`, `tar -cvzf`

### Exercises

-   What is the output of the closing `ls` command in the sequence shown below?

<code>
    $ pwd
    
    /home/thesis/data
    
    $ touch proteins.dat
    
    $ ls
    
    proteins.dat
    
    $ mkdir recombine
    
    $ mv proteins.dat recombine
    
    $ cp recombine/proteins.dat ../proteins-saved.dat
    
    $ ls
</code>

-   Suppose that:
<code>
    $ ls -F
    
    analyzed/  fructose.dat    raw/   sucrose.dat
</code>
    
What command(s) (such as `rm`, `mv`) could you run so that the commands below will produce the output shown?

<code>
    $ ls
    
    analyzed   raw
    
    $ ls analyzed
    
    fructose.dat    sucrose.dat
</code>

3. What does `cp` do when given several filenames and a directory name, as in:

<code>
    $ mkdir backup
    
    $ cp thesis/citations.txt thesis/quotations.txt backup
</code>
    
What does `cp` do when given three or more filenames, as in:
    
<code>
    $ ls -F
    
    intro.txt    methods.txt    survey.txt
    
    $ cp intro.txt methods.txt survey.txt
</code>
    
Why do you think `cp`'s behavior is different from `mv`'s?

-   The command `ls -R` lists the contents of directories recursively,
    _i.e._, lists their sub-directories, sub-sub-directories, and so on
    in alphabetical order at each level. The command `ls -t` lists things
    by time of last change, with most recently changed files or
    directories first. In what order does `ls -R -t` display things?


## Pipes & filters
-   Redirect a command's output to a file.
-   Process a file instead of keyboard input using redirection.
-   Construct command pipelines with two or more stages.
-   Explain what usually happens if a program or pipeline isn't given any input to process.
-   Explain Unix's "small pieces, loosely joined" philosophy.

-   `command > file` redirects a command's output to a file.
-   `first | second` is a pipeline: the output of the first command is used as the input to the second.
-   The best way to use the shell is to use pipes to combine simple single-purpose programs (filters).

-   `|`, `>`, `<`, `&>`

### Advanced
-   `2>`, `<<`

-   `tr a-z A-Z << END_TEXT`

-   `one two three`

-   `um dois três`

-   `END_TEXT`

-   `>>`

### Exercises

-   The following command will invoke a program called Git to download some Python files.
        git clone https://github.com/uiuc-cse/rankine.git
    Execute this line and then go into the directory and list its contents.
    These scripts are designed to input and output their data through streams.
    For instance, execute `python grab-stations.py` and observe the output.
    -   How can we capture this output as a file?
    -   The programs are designed to work in series:
        `grab-stations.py` feeds data to `grab-forecast.py` which feeds into `plot-forecast.py`.
        Write a single line command to effect this entire process.
<code>
    python grab-stations.py > stations.txt
    
    python grab-forecast.py < stations.txt > forecast.txt
    
    python plot-forecast.py < forecast.txt
</code>

(Navigate to the data/pipes/ directory for the following examples.)

-   If we run sort on the file `numbers.txt`, what is the output?  If we run
    `sort -n` on the same input, what do we get instead?  Explain why `-n`
    has this effect.

-   What is the difference between

        $ wc -l < mydata.dat

    and

        $ wc -l mydata.dat

-   The command `uniq` removes adjacent duplicated lines from its input.
    For example, run the following commands:
    
        $ cat salmon.txt
        
        $ uniq salmon.txt
    
    Why do you think `uniq` only removes adjacent duplicated lines? (Hint: think about very large data sets.) Which other command could you combine with it in a pipe to remove all duplicated lines?

-   Examine the file called `animals.txt` using less.  What text passes through
    each of the pipes and the final redirect in the pipeline below?

        cat animals.txt | head -5 | tail -3 | sort -r > final.txt

-   The command:
    
        $ cut -d , -f 2 animals.txt
    
    produces the following output:

        deer
    
        rabbit
    
        raccoon
    
        rabbit
    
        deer
    
        fox
    
        rabbit
    
        bear
    
    What other command(s) could be added to this in a pipeline to find out what
    animals the file contains (without any duplicates in their names)?


## Loops
-   Write a loop that applies one or more commands separately to each file in a set of files.
-   Trace the values taken on by a loop variable during execution of the loop.
-   Explain the difference between a variable's name and its value.
-   Explain why spaces and some punctuation characters shouldn't be used in files' names.
-   Demonstrate how to see what commands have recently been executed.
-   Re-run recently executed commands without retyping them.

-   A `for` loop repeats commands once for every thing in a list.
-   Every `for` loop needs a variable to refer to the current "thing".
-   Use `$name` to expand a variable (i.e., get its value).
-   Do not use spaces, quotes, or wildcard characters such as `*` or `?` in filenames, as it complicates variable expansion.
-   Give files consistent names that are easy to match with wildcard patterns to make it easy to select them for looping.
-   Use the up-arrow key to scroll up through previous commands to edit and repeat them.
-   Use `history` to display recent commands, and `!number` to repeat a command by number.

-   `for`, `do`, `done`
-   `if`, `then`, `fi` [ref](http://www.tldp.org/LDP/Bash-Beginners-Guide/html/sect_07_01.html)
    
        for i in {a..z}  # only way to do non-numeric lists

        do               # try also with {A..z} to show trouble

            echo $i

        done

-   Ctrl + C

### Advanced
-   `ps`
    -   `ps -aux`
    -   `kill -9 <pid>`
-   `$()`

### Exercises
-   Suppose that `ls` initially displays:
    
        fructose.dat    glucose.dat   sucrose.dat
    
    What is the output of:
    
        for datafile in *.dat
        do
            ls *.dat
        done

-   In the same directory, what is the effect of this loop?
    
        for sugar in *.dat
        do
            echo $sugar        
            cat $sugar > xylose.dat        
        done
    
    1. Prints fructose.dat, glucose.dat, and sucrose.dat, and copies sucrose.dat to create xylose.dat.
    2. Prints fructose.dat, glucose.dat, and sucrose.dat, and concatenates all three files to create xylose.dat.
    3. Prints fructose.dat, glucose.dat, sucrose.dat, and xylose.dat, and copies sucrose.dat to create xylose.dat.
    4. None of the above.

-   `expr` does very simple arithmetic using command-line parameters:
    
        $ expr 3 + 5
    
        8
    
        $ expr 30 / 5 - 2
    
        4
    
    Given this, what is the output of:
    
        for left in 2 3
        do
            for right in $left
            do
                expr $left + $right
            done
        done

-   What is the problem with multiplication with `expr`?  Can you _escape_ the `*` so that it works as expected?


## Shell Scripts
-   Write a shell script that runs a command or series of commands for a fixed set of files.
-   Run a shell script from the command line.
-   Write a shell script that operates on a set of files defined by the user on the command line.
-   Create pipelines that include user-written shell scripts.

-   Save commands in files (usually called shell scripts) for re-use.
-   `bash filename` runs the commands saved in a file.
-   `$*` refers to all of a shell script's command-line parameters.
-   `$1`, `$2`, etc., refer to specified command-line parameters.
-   Letting users decide what files to process is more flexible and more consistent with built-in Unix commands.

-   `#`
-   `export`
-   `sudo`

-   `head`
    -   `head -20 cholesterol.pdb | tail -5 | sort`
    -   `head -1 srtd`
-   `tail`
-   (now pipe together)
-   `bash middle.sh`

-   Now let's turn that into an arbitrary slicer:
    
        head $2 $1 | tail $3
    
        # Select lines from the middle of a file.
    
        # Usage: middle.sh filename -end_line -num_lines
    
        head $2 $1 | tail $3
    
    
        # Select lines from the middle of a file.
    
        # Usage: middle.sh filename -first_line -last_line
    
        head -$3 $1 | tail -$(expr $3 - $2 + 1)

### Advanced
-   `.bash_profile`
-   `alias`
-   `at`, `atq`
-   `#!/usr/bin/bash`
-   `chmod +x`

### Exercises
-   Leah has several hundred data files, each of which is formatted like this:
    
        2013-11-05,deer,5
    
        2013-11-05,rabbit,22
    
        2013-11-05,raccoon,7
    
        2013-11-06,rabbit,19
    
        2013-11-06,deer,2
    
        2013-11-06,fox,1
    
        2013-11-07,rabbit,18
    
        2013-11-07,bear,1
    
    Write a shell script called `species.sh` that takes any number of
    filenames as command-line parameters, and uses `cut`, `sort`, and `uniq`
    to print a list of the unique species appearing in each of those files
    separately.  (Test this on the files in `data/pipes/animals`)

-   Write a shell script called `longest.sh` that takes the name of a directory
    and a filename extension as its parameters, and prints out the name of the
    most recently modified file in that directory with that extension. For example:
    `$ bash largest.sh /tmp/data pdb`
    would print the name of the `.pdb` file in `/tmp/data` that has been changed
    most recently.

-   If you run the command:
    `history | tail -5 > recent.sh`
    the last command in the file is the `history` command itself, _i.e._, the
    shell has added `history` to the command log before actually running it.
    In fact, the shell always adds commands to the log before running them.
    Why do you think it does this?

-   Joel's data directory contains three files: `fructose.dat`, `glucose.dat`,
    and `sucrose.dat`. Explain what the following script, `example.sh`, would
    do when run as `bash example.sh *.dat`:
    
        echo *.*
    
        for filename in $1 $2 $3
    
        do
    
            cat $filename
        
        done
    
        echo $*.dat

-   The `history` shows the last thousand or so commands that you've used.  What does this
    code do?  (Test `awk '{print $1}' data/pdb/methane.pdb` to see what this `awk` does.)
    
    `awk '{print $1}' ~/.bash_history | sort | uniq -c | sort -n | tail -10 | sort -n -r`

## Finding Things
-   Use grep to select lines from text files that match simple patterns.
-   Use find to find files whose names match simple patterns.
-   Use the output of one command as the command-line parameters to another command.
-   Explain what is meant by "text" and "binary" files, and why many common tools don't handle the latter well.

-   Use find to find files and directories, and grep to find text patterns in files.
-   `$(command)` inserts a command's output in place.
-   man command displays the manual page for a given command.

-   `wc`, `wc -l`, `wc -w`, `wc -c`
    -   wc -l *.pdb > len
-   `cut`

-   `grep <txt> <file>`
    -   `grep -r <txt> <fl/>`
-   `ls len`

-   `find`
-   `cat len`

### Exercises

-   Write a short explanatory comment for the following shell script:

<code>
    $ find . -name '*.dat' -print | wc -l | sort -n
</code>

-   The `-v` flag to grep inverts pattern matching, so that only lines which
    _do not_ match the pattern are printed.  Given that, which of the following
    commands will find all files in `data/chem/pdb` whose names end in `ose.dat`
    (_e.g._, `sucrose.dat` or `maltose.dat`), but do not contain the string `temp`?
    
    1. `$ find data/chem/pdb -name '*.pdb' -print | grep ose | grep -v temp`
    2. `$ find data/chem/pdb -name ose.pdb -print | grep -v temp`
    3. `$ grep -v temp $(find data/chem/pdb -name '*ose.pdb' -print)`
    4. None of the above.

![](./img/xkcd-cautionary.png)

### Advanced
-   `at`, `atq`
-   `expr`
-   `#!/usr/bin/bash`
-   `chmod +x`
-   `!!` executes last command again

-   `top`
-   `w`
-   `nohup`

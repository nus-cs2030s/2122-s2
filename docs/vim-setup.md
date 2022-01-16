# Setting Up `vim` on PE Hosts

Like many other Unix programs, you can configure your preferences by creating an `rc` (run commands) file in your home directory.  These `rc` files will be read by the corresponding programs and executed line-by-line as if the text is entered into the program through a keyboard.  You can view these `rc` as a script that will be executed automatically whenever a program starts.

For `vim`, the `rc` file is called `.vimrc`.  The `.` in the front of the file name carries a special meaning in Unix.  It means that this file is hidden -- you won't see it when you `ls`.  Hiding the run command files prevent your home directory from being cluttered.  To tell `ls` to show the hidden files, use the `-a` flag
```
$ ls -a
```

We have created a `.vimrc` file, with CS2030S defaults, for your use.  This is the basis which you can built on. 

To copy this file to your home directory on the PE nodes,
```
$ cp ~cs2030s/.vimrc ~
```

You can ask `vim` to automatically backup files that you edit.  This has been a lifesaver for me on multiple occasions.

The default `.vimrc` contains the following two lines:

```
set backup
set backupdir=~/.backup
```

This causes `vim` to save the previous version of every file you edited in a backup directory at location `~/.backup`.  You need to create this directory, however, by

```
$ mkdir ~/.backup
```

Now, if you made changes to a file that you regretted, or if you accidentally deleted a file, you can check under `~/.backup` to see if the backup can save you.

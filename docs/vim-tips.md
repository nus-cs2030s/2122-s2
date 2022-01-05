# Vim Tips

I collected some tips on `vim` that I find helpful.  If you are new to `vim`, please try out the command `vimtutor` on any machine where `vim` is installed, and check out the nice article [Learn vim Progressively](
http://yannesposito.com/Scratch/en/blog/Learn-Vim-Progressively/).  

## 1. Useful Configuration

You can configure your `vim` by putting your configuration options and scripts in the `~/.vimrc` file (a hidden file named `.vimrc` in your home directory).  This file will be loaded whenever you start `vim`.

You can copy a sample `.vimrc` file from `~cs1010/.vimrc` to your home directory.
You can edit this file `~/.vimrc` just like any other file, using `vim`.

### Help

In `vim,` the command `:help <topic>` shows help about a particular topic in `vim`.  Example, `:help backup`.


### Syntax Highlighting

If for some reasons, syntax highlighting is not on by default, add this to your `~/.vimrc`:

```
syntax on
```

### Ruler and Numbers

If you prefer to show the line number you are on and the column number you are on, adding the commands to `~/.vimrc`

```
set ruler
```

will display the line number and the column number on the lower right corner.  

You can also add
```
set number
```

to label each line with a line number.

### Auto Indentation

Proper indentation is important to make your code readable (to yourself and others).  You should enable this in `vim` with:

```
set autoindent
set smartindent
```

Autoindent will cause the next line to have the same indentation as the previous line; while smartindent has some understanding of C-like syntax (such as recognizing `{` and `}`) and indent your code accordingly.  The size of the indentation is based on the setting `shiftwidth`.  For CS1010, please set it to either `2` or `4`:

```
set shiftwidth=2
```

## 2. Navigation

### Basic Navigation

Use ++k++ and ++j++ keys to move up and down (just like Gmail and Facebook!).  ++h++ and ++l++ to move left and right.

Other shortcuts (no need to memorize them now, just refer back when you feel like you are typing too many ++h++++j++++k++++l++ to see how you can navigate faster).

- ++w++ jump to the beginning of the next word
- ++b++ ump to the beginning of the previous word (reverse of `w`)
- ++e++ jump to the end of the word (or next word when pressed again)
- ++f++ char: search forward in the line and sit on the next matching char
- ++t++ char:  search forward in the line and sit on one space before the matching char
- ++shift+4++ ($) jump to the end of line
- ++0++ jump to the beginning of the line
- ++shift+6++ (^) jump to the first non-blank character of the line
- ++shift+5++ (%) jump between matching parentheses
- ++control+d++ jump forward (Down) half page
- ++control+f++ jump Forward one page
- ++control+u++ jump backward (Up) half page
- ++control+b++ jump Backward half page

### Jumping to a Line

If the compiler tells you there is an error on Line $x$, you can issue `:<x>` to jump to Line $x$.  For instance, `:40` will go to Line 40.

## 3. Editing Operations

### Undo

Since we are on the topic of correcting mistakes, ++u++ in command mode undo your changes.  Prefix it with a number $n$ to undo $n$ times.  If you want to undo your undo, ++control+r++ will redo.

### Navigation + Editing

`vim` is powerful because you can combine _operations_ with _navigation_.  For instance ++c++ to change, ++d++ to delete, ++y++ to yank (copy).  Since ++w++ is the navigation command to move over the current word, combining them we get:

- ++c++++w++ change the current word (delete the current word and enter insert mode)
- ++d++++w++ delete the current word
- ++y++++w++ yank the current word (copy word into buffer)

Can you guess what each of these do:

- ++d++++f++++shift+0++ 
- ++d++++f++++shift+0++ 
- ++c++++shift+4++
- ++y++++0++

If you repeat the operation ++c++, ++d++, and ++y++, it applies to the whole line, so:

- ++c++++c++ change the whole line
- ++d++++d++ delete the whole line
- ++y++++y++ yank the whole line

You can add a number before an operation to specify how many times you want to repeat an operation.  So ++5++++d++++d++  deletes 5 lines, ++5++++d++++w++ deletes 5 words, etc.

See the article [Operator, the True Power of `Vim`](http://whileimautomaton.net/2008/11/vimm3/operator) for more details.

### Swapping Lines

Sometimes you want to swap the order of two lines of code, in command mode, ++d++++d++++p++ will do the trick.  ++d++++d++ deletes the current line, ++p++ paste it after the current line, in effect swapping the order of the two lines.

### Commenting blocks of code

Sometimes we need to comment out a whole block of code in C for testing purposes. There are several ways to do it in `vim`:

- Place the cursor on the first line of the block of code you want to comment on.
- ++0++ to jump to the beginning of the line
- ++shift+v++ enter visual mode
- Use the arrow key to select the block of code you want to comment on.
- ++shift+i++ to insert at the beginning of the line (here, since we already selected the block, we will insert at the beginning of every selected)
- ++slash++++slash++ to insert the C comment character (you will see it inserted in the current line, but don't worry)
- ++escape++ to escape from the visual code.

To uncomment,

- Place the cursor on the first line of the block of code you want to comment.
- ++0++ to jump to the beginning of the line
- ++control+v++ enter block visual mode
- Use the arrow key to select the columns of text containing `//`
- ++x++ to delete them

## 4. Other Useful Commands

### Search and Replace in `vim`

```
:%s/oldWord/newWord/gc
```

`:` enters the command mode.  `%` means apply to the whole document, `s` means substitute, `g` means global (otherwise, only the first occurrence of each line is replaced). `c` is optional -- adding it cause `vim` to confirm with you before each replacement  

### Shell Command

If you need to issue a shell command quickly, you don't have to exit `vim`, run the command, and launch `vim` again.  You can use `!`,

```
:!<command>
```

will issue the command to shell.  E.g.,

```
:!ls
```

You can use this to compile your current file, without exiting `vim`.

```
:!make
```

`make` is actually a builtin command for `vim` so you can also simply run

```
:make
```

### Abbreviation

You can use the command `ab` to abbreviate frequently typed commands.  E.g., in your `~/.vimrc`,

```
ab pl cs1010_print_long(
```

Now, when you type `pl `, it will be expanded into `cs1010_print_long(`

### Auto-Completion

You can use ++control+p++ or ++control+n++ to auto-complete.  By default, the autocomplete dictionary is based on the text in your current editing buffers.  This is a very useful keystroke saver for long function and variable names.

### Auto-Indent the Whole File

You can ++g++++g++++equal++++shift+g++ in command mode (i.e., type out `gg=G`) to auto-indent the whole file.  ++g++++g++ is the command to go to the beginning of the file.  ++equal++ is the command to indent.  ++shift+g++ is the command to go to the end of the file.

### Splitting `vim`'s Viewport

- `:sp file.c` splits the `vim` window horizontally
- `:vsp file.c` splits the `vim` window vertically
- ++control+w++++control+w++ moves between the different `vim` viewports

### Jump to `Foo.java`

Place your cursor on the class name, e.g., `Foo`.  Then hit ++g++ ++f++.

## 5. Color Schemes

We have installed [`vim-colorscheme`](https://github.com/flazz/vim-colorschemes) bundle under `~cs2030s/.vim/vim-colorschemes/colors`.

Run

```
mkdir -p ~/.vim
ln -s ~cs2030s/.vim/vim-colorschemes/colors ~/.vim/colors
```

After that, your can change your vim color scheme as usual.  For instance,

```
:color gruvbox
```

You can add the line `color gruvbox` to your `~/.vimrc` so that the color scheme is loaded at the start of every vim session.

The bundle includes some of the popular color schemes among students, such as `molokai`, `solarized`, and `gruvbox`.   Some color schemes display differently depending on whether the background is set to `dark` or `light`

Some examples, with `set background=dark` in `~/.vimrc`:

The default color scheme:

![default](figures/color-scheme-default.png)

The molokai color scheme:

![molokai](figures/color-scheme-molokai.png)

The gruvbox color scheme 

![gruvbox](figures/color-scheme-gruvbox.png)

## 6. Recovery Files

Vim automatically saves the files you are editing into temporary _swap_ files, with extension `.swp`.  These files are hidden so you don't normally see them when you run `ls`.  (You need to run `ls -a` to view the hidden files)

The swap files are useful if your editing session is disrupted before you save (e.g., the network is disconnected, you accidentally close the terminal, your OS crashes, etc.).

When you launch `vim` to edit a file, say, `foo.c`.  `vim` will check if a swap file `.foo.c.swp` exist.  If it does, `vim` with display the following

```
Found a swap file by the name ".foo.c.swp"
		  owned by: elsa   dated: Sat Aug 21 15:01:04 2021
		 file name: ~elsa/foo.c
          modified: no
		 user name: elsa   host name: pe116
        process ID: 7863 (STILL RUNNING)
While opening file "foo.c"
             dated: Mon Jul 12 18:38:37 2021

(1) Another program may be editing the same file.  If this is the case,
    be careful not to end up with two different instances of the same
    file when making changes.  Quit, or continue with caution.
(2) An edit session for this file crashed.
    If this is the case, use ":recover" or "vim -r a.c"
    to recover the changes (see ":help recovery").
    If you did this already, delete the swap file ".a.c.swp"
    to avoid this message.

Swap file ".a.c.swp" already exists!
[O]pen Read-Only, (E)dit anyway, (R)ecover, (Q)uit, (A)bort:
```

The messages above is self-explanatory.  Read it carefully.  Most of the time, you want to choose "R" to recover your edits, so that you can continue editing.  Remember to remove the file `.foo.c.swp` after you have recovered.  Otherwise `vim` will prompt you the above messages every time you edit `foo.c`.

Warning: if `foo.c` is newer than the state saved in `.foo.c.swp`, and you recover from `.foo.c.swp`, you will revert back to the state of the file as saved in the swap file.  This can happen if (i) you edit the file without recovery, or (ii) you recover the file, continue editing, but did not remove the `.foo.c.swp` file after.

## Learning More

To learn more about `vim`, we suggest that you run `vimtutor` on the command line and follow through the tutorials.

You can always `:help <keywords>` to search for the built-in help pages within `vim`.

Once you are comfortable, you can soup up your `vim` with [various plugins](vim-plugins.md) and learn how to use advanced commands (such as recording macros, folding) that are invaluable for programming.

There are also many video tutorials and resources online, in addition to the [introduction to vim](https://mediaweb.ap.panopto.com/Panopto/Pages/Viewer.aspx?id=85be23af-8b65-4d5f-a164-acaa001edc74) by Yong Qi that we have shared earlier, some interesting ones are:

- [Vim: Precision Editing at the Speed of Thought](https://vimeo.com/53144573): A talk by Drew Neil
- [Vim Adventure](https://www.vim-adventures.com): An adventure game for learning `vim`
- [Vim Casts](http://vimcasts.org/episodes/archive/): Videos and articles for teaching `vim`
- [Vim Video Tutorials](http://derekwyatt.org/vim/tutorials/) by Derek Wyatt
- [Vim Awesome](https://vimawesome.com/): Directory of plugins.

# Tools

## Editors
**Emacs** and **vim** are the two standard editors which work via terminal.
## Emacs Shortcuts
Access the Emacs reference card [here](https://www.gnu.org/software/emacs/refcards/pdf/refcard.pdf).
- *Ctrl-K*: cuts the line
- *Ctrl-Y*: pastes the line
- *Ctrl-Space*: starts highlighting, move arrows, then *Esc-W* to copy. 
- *Ctrl-X* then the number. It opens multiple "buffers", or sub window. 
	- *Ctrl-X-O* jumps between buffers with . 
	- *Ctrl-X-F* to point your buffer to another file. Provide the relative file. 
- *Ctrl-X-S* saves the file.  
- *Ctrl-X-C* quits Emacs.

## gdb
`gdb` is a GNU debugger that allows you to:
- flexibly *pause* and *resume*
- print out values of variables mid-stream
- see where severe errrors like `Segmentation Faults` happen. 
- When using `gdb` or `valgrind`, compile with `-g`, which packages up the source code ("debug symbols") along with the executable. 

### Commands
 `break main` sets a break point (where you want to stop the execution) at the beginning of the main functions. 
`run` continues execution.
`next` executes the statement on the current line and moves onto the next and then stops. Use the shortcut `n`.
`step` begins to execute the statement on the current line. If the statement contains a function call, it *steps into* the function and pauses there.
`print <variable-name>` prints out the value of the variable. `p` is the shotcut. 

## Valgrind
`valgrind` is a debugging tool for finding memory usage mistakes such as:
- invalid memory accesses: e.g. array index out of bounds
- memory leaks: failure to `free` dynamically-allocated memory (`HEAP SUMMARY`).
- invalid read and writes: attempts to dereference pointers to memory that is not yours. 

### How to use valgrind?
1. Compile program with the flag `-g`
2. Run the program with 
`
valgrind --leak-check=full ./myFile <arg1> <arg2> ...
`
3. Look for `All heap bocks were freed` and `ERROR SUMMARY: 0 errors` for no issues.
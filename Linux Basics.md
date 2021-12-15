# Linux Basics

## Unix/Linux
They are designed to support the need of programmers. They are a powerful class of operating systems, multiuser, unified file system that names files and directories, heavily based on command-line interface called the "shell". 
They are designed to automate tasks. Put in upfront effort to reduce the manual effort needed later, called "long-term lazy" (slower to learn, faster to use). 

*Directory* means the same thing as *folder*. All files and directories are referred to names called "paths". 
- `~` denotes the home directory of your account
- `.` denotes the current directory
- `..` denotes the parent directory (one level up from current)
- When you log into ugrad, you'll be in your home directory.

## Connecting to ugrad from your own computer
Windows: download PuTTy, set Host Name as `ugradx.cos.jhu.edu`, type account name (JHED), and password.
Mac: open Terminal, then type the command `ssh <your-username>@ugradx.cs.jhu.edu`
Linux: open terminal and use `ssh <your-username>@ugradx.cs.jhu.edu`.

## Command Line
Unix/Linux commands are case-sensitive.
Learn Unix/Linu command line from this [boot camp](https://cli-boot.camp).

### Basic Commands
- `pwd` - print working directory
- `ls` - list directory contents
- `cd <folder_name>` - change directory [specify directory name]
- `mkdir <folder_name>` makes a new directory within current directory.
- `less <file_to_view>` view text file screenful at a time.
- `mv <source> <destination>` changes the location of file or folder.
- `cp <source> <destination>` make a copy file or folder.
- `rm <file_to_remove>` remove a file. Not easy to undo deletion.
	- Use the flag `-r` to delete recursively and remove subdirectories and `-i` if you want to verify deletion. 
- Loations can be *relative* to current directory (E.g.: `cp Hello.c folderForToday/hello.c`) or *absolute*, based on the full path in file system.
- `exit` logs out of the ugrad system.
- `man` is the manual available at command line. Using with an operation or function gets details (e.g,  `man cp` or `man ispunct`).

## Copying Files
`cp` command in Unix is how we copy files within one machine. 
`scp` and `pscps` command is *secure* copy, a way to transfer copies from one machine to another. 

In Mac Terminal or Windows Power Shell, use `scp <source> <destination>`.

In Windows with PuTTY, use `pscp <source> <destination>` in Command Prompt. 
- Note that Windows machine use backslash (`\`) instead of forward slash (`/`) used in unix for file paths. 

### Ugrad to Local
```
scp <username>@ugradx.cs.jhu.edu:<filename>.c .
```
(in Mac Terminal or Windows Power Shell).

For example,
```
scp ltran29@ugradx.cs.jhu.edu:HW1/file.c xyz/
```

## Zipping
```
zip zipped_files.zip file1.c file2.c gitlog.txt
```
Packs up three files into a `zipped_files.zip`.

To confirm that it contains what you want,
```
unzip -1 zipped_files.zip
```

To unpack the zip file (i.e., extract its file),
```
unzip zipped_files.zip
```

Move and unpack in a new/different folder to avoid overwriting the original files. 

## I/O Redirection
When executing a command that produces output, redirect the result to a textfile (instead of on screen) by using '`>` outfile':
```
ls > myfiles.txt
```

When executing a command that takes input, redirect input from a plain txt file by using '`<` infile':
```
less < infile.text
```

Use both at once, or use a pipe command '`|`' to send the standard output of one command directly into standard inputfor another command. For example, to list your files but view the list one screenful at a time use:
```
ls | less
```
- `echo 4 | ./a.out` sends an input directly into a program. 

## Homework workflow
1. Write code, compile, test, and edit while continuously adding, committing, and pushing changes to personal git repo.
2. Generate `gitlog.txt` file to document your commits using `git log > gitlog.txt`.
3. Bundle files for submission with `zip hw0.zip file1.c file2.c gitlog.txt`.
4. Confirm that your zip files contains everything with `unzip -1 hw0.zip`.
5. Transfer the bundle onto local machine using `scp <username>@ugradx.cs.jhu.edu:<HW0/hw0.zip .`
6. Upload `hw0.zip` to Gradescope. Wait for feedback and resubmit (only last one is graded).

## Tips
- `*`: wildcard character, helpful with file commands. 
	- `git add *.c*` adds all files ending in .c to your staging area. 
	- `ls f*` lists all files that start with f.
- `!` (bang): repeats the prior command. Can be used alone or with a start of a command name. 
	- `! !` will execute the prior command. 
	- `!em` will execute the most recent command that started with "em"	 
- up and down arrows cycles through your command history
- tab will complete command. 
- `history | grep <keyword>`: searches history with keyword. 
- 
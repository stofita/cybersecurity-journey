# Linux notes

## What is Linux?
Linux is an open-source OS. It contains many different distros (distributions), each characterized by different utilities and flexibility.

The kernel is the core of the operating system. It manages important resources (RAM and CPU) and links the hardware and software parts.

Right now I'm using Ubuntu because it's beginner-friendly and it will facilitate my learning curve.

## Paths
There are two kinds of paths:

- **Absolute path:** starts with `/`, the root of the system. It's the complete route.
  Example: `/home/stofita/notes`
  
- **Relative path:** does not start with `/`. It is read from the folder I'm in now. `./` means "the current folder" and is optional.
  Example: from `/home`, both `cd stofita` and `cd ./stofita` do the same thing.

## Commands learned so far

| Command | What it does | Example |
|---------|--------------|---------|
| `pwd` | Print Working Directory, shows where I am | `pwd` |
| `cd` | Changes the directory | `cd testdir` |
| `cd .` | Current directory | `cd .` |
| `cd ..` | Parent directory | `cd ..` |
| `cd ~` | Home directory | `cd ~` |
| `cd -` | Previous directory | `cd -` |
| `echo` | Prints the text after it, like `printf` in C | `echo "Hello"` |
| `echo "text" > file` | Writes text to a file (overwrites it) | `echo "Hello" > file1.txt` |
| `echo "text" >> file` | Appends text to a file | `echo "More" >> file1.txt` |
| `mkdir` | Creates a directory | `mkdir testdir` |
| `touch` | Creates an empty file, or updates the timestamp of an existing one | `touch file1.txt` |
| `cp` | Copies a file | `cp file1.txt testdir/` |
| `cp -r` | Copies a directory and its content (recursive) | `cp -r mydir mydir_copy` |
| `mv` | Renames or moves a file or directory | `mv old.txt new.txt` |
| `rm` | Removes files | `rm file1.txt` |
| `rm -r` | Removes a directory and its content | `rm -r testdir` |
| `rm -i` | Asks for confirmation before deleting | `rm -i file1.txt` |
| `file` | Shows the type of a file's content | `file file1.txt` |
| `file -i` | Shows the MIME type | `file -i file1.txt` |
| `ls` | Lists files in the current directory | `ls` |
| `ls -a` | Includes hidden files (names starting with `.`) | `ls -a` |
| `ls -l` | Long format: permissions, owner, size, date | `ls -l` |
| `ls -lh` | Long format with human-readable sizes | `ls -lh` |

### Caution
`rm -rf` deletes without asking, and there is no recycle bin. I use `rm -i` while learning.

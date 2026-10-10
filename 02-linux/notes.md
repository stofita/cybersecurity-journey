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

## Commands by task

### Where am I? Moving around
| Command | What it does |
|---------|--------------|
| `pwd` | Shows where I am |
| `cd dir` | Changes directory |
| `cd ..` / `cd ~` / `cd -` | Parent / home / previous directory |
| `ls` | Lists files (`-a` hidden, `-l` details, `-lh` readable sizes) |

### Creating and organizing
| Command | What it does |
|---------|--------------|
| `mkdir dir` | Creates a directory |
| `touch file` | Creates an empty file (or updates its timestamp) |
| `cp file dir/` | Copies a file (`-r` for a directory) |
| `mv old new` | Renames or moves |
| `rm file` | Removes a file (`-r` directory, `-i` ask first) |

### Reading files
| Command | What it does |
|---------|--------------|
| `cat file` | Shows the content (`-n` adds line numbers) |
| `head file` | First 10 lines (`-n 1` for just one) |
| `tail file` | Last 10 lines (`-f` follows live, useful for logs) |
| `less file` | Interactive reading (`/word` to search, `q` to quit) |

### Writing and comparing
| Command | What it does |
|---------|--------------|
| `echo "text" > file` | Writes text to a file (overwrites) |
| `echo "text" >> file` | Appends text to a file |
| `diff f1 f2` | Shows the lines that differ (`-r` for directories) |
| `file f` | Shows the content type (`-i` MIME type) |

### History and terminal
| Command | What it does |
|---------|--------------|
| `history` | Shows the command history (`-c` clears memory, `-d N` deletes entry N, `-w` writes it to the history file) |
| `clear` | Clears the terminal screen |

### Permissions and ownership
| Command | What it does |
|---------|--------------|
| `chmod u+x file` | Changes permissions (`u` owner, `g` group, `o` others, `a` all, with `+` add, `-` remove, `=` set) |
| `chmod 755 file` | Same with numbers: r=4, w=2, x=1, in the order owner, group, others |
| `sudo chown user:group file` | Changes the owner and group of a file (only root can change the owner) |
| `#!/bin/bash` | Shebang, the first line of a script. It tells the system which interpreter runs it. |

### Users and groups
| Command | What it does |
|---------|--------------|
| `sudo adduser name` | Creates a user, with a home folder and a password prompt (`useradd -m` is the low-level version) |
| `sudo usermod -aG group name` | Adds a user to a group (`-a` append, `-G` group). Never use `-G` without `-a`. |
| `sudo passwd -l name` | Locks an account (`-u` unlocks it) |
| `sudo userdel -r name` | Deletes a user and their home folder |

## Mistakes I made / things to remember
- `rm` alone doesn't delete directories, so I need `-r`.
- `>` overwrites a file, while `>>` appends.
-  `history` can contain passwords I typed on the command line, so never type secrets directly into commands.
- `chmod 777` makes a file writable by everyone, and I don't use it.
- Give `sudo` only to users who truly need it (least privilege).

### Caution
`rm -rf` deletes without asking, and there is no recycle bin. I use `rm -i` while learning.

## OverTheWire Bandit progress
- Levels 0-5 completed (basic navigation, reading files, hidden files, file types).
- Next: levels 6-10 (searching for files, text processing).
- Biggest lesson so far: reading `man` pages first saves time.

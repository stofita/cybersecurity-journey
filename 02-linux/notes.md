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

- `echo`: prints the text after it, like `printf` in C.
- `pwd`: Print Working Directory, shows where I am (the current location).
- `cd`: changes the directory. Shortcuts:
  - `cd .` current directory
  - `cd ..` parent directory
  - `cd ~` home directory
  - `cd -` previous directory

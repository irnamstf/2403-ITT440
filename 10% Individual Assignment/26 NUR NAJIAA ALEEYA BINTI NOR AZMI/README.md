# How to Install GCC Compiler using pkg Package Manager on FreeBSD

## Introduction
GCC or "GNU Compiler Collection" isa free software compiler system capable of compiling several programming languages, including C, C++, Objective-C, and Fortran. GCC is widely used in creating software for Unix-like systems, such as Linux, Windows, various BSDs. It has been adapted for various platforms, demonstrating its adaptability and flexibility in the realm of open-source programming.

## How Does It Work?
GCC is a toolchain that compiles code, links it with any library dependencies, converts that code to assembly, and then prepares executable files. It follows the standard UNIX design philosophy of using simple tools that perform individual tasks well. The GCC development suite utilizes these discrete tools to compile software.

When you run GCC on a source code file, it first uses a preprocessor to include header files and discard comments. Next, it tokenizes the code, expands macros, detects any compile-time issues, then prepares it for compilation. It is then sent to the compiler, which creates syntax trees of the program’s objects and control flow and uses those to generate assembly code. The assembler then converts this code into the binary executable format of the system. Finally, the linker includes references to any external libraries as needed. The finished product is then executable on the target system.

## Prerequisites
Before we start the installation, make sure you have everything you need:

1. A running FreeBSD System: You will need a working FreeBSD operating system. If you haven't installed FreeBSD yet, you can find installation guides on the official FreeBSD website.
   
2. Access to the Terminal: Familiarize yourself with the FreeBSD terminal. It's the command-line interface where we will execute te installation commands.

3. Sudo privileges: Ensure that you have sudo privileges. You will need these to install software and make system changes.
   
4. Internet connection: Make sure you have an active internet connection. The installation of GCC are depends on online repositories.

5. Storage Space: Ensure that you have enough free storage space on your FreeBSD system. GCC and its associated libraries may require a few hundred megabytes of space.


### Step 1: Open terminal on FreeBSD
The terminal takes the input from the user in the form of commands and displays the output on the screen. 

### Step 2: Update package repository
To update package repository, use the following command:
  ```
  sudo pkg update
  ```
This command is used to download package information from all configured sources and to get the info of the updated versions of the packages. Example:
```c
root@najiaa:~ # sudo pkg update
Updating FreeBSD repository catalogue...
FreeBSD repository is up to date.
All repositories are up to date.
```

### Step 3: Install GCC 
To install GCC, use the following command:
  ```
  sudo pkg install gcc
  ```

Example:
```c
root@najiaa:~ # sudo pkg install gcc
Updating FreeBSD repository catalogue...
FreeBSD repository is up to date.
All repositories are up to date.
Checking integrity... done (0 conflicting)
The following 2 package(s) will be affected (of 0 checked):

New packages to be INSTALLED:
        gcc: 13_5
        gcc13: 13.2.0_4

Number of packages to be installed: 2
The process will require 319 MiB more space.
Proceed with this action? [y/N]: y
[1/2] Installing gcc13-13.2.0_4...
[1/2] Extracting gcc13-13.2.0_4: 100%
[2/2] Installing gcc-13_5...
[2/2] Extracting gcc-13_5: 100%
=====
Message from gcc13-13.2.0_4:
--
To ensure binaries built with this toolchain find appropriate versions
of the necessary run-time libraries, you may want to link using
  -Wl,-rpath=/usr/local/lib/gcc13
For ports leveraging USE_GCC, USES=compiler, or USES=fortran this happens
transparently.
```

### Step 4: Verify GCC installation
To verify if GCC has been installed, use the following command:
  ```
  gcc --version
  ```

Example:
```c
root@najiaa:~ # gcc --version
gcc (FreeBSD Ports Collection) 13.2.0
Copyright (C) 2023 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```
The system has confirmed GCC version 13.2.0 is successfully installed!

## Conclusion
Installation GCC on FreeBSD invloves navigating to the appropriate directory and compiling the software. By following the outlined steps, you ensure a successful installation, equipping your system with a powerful set of compilers for various programming languages. With GCC installed, you are now ready to compile and build software projects efficiently on your FreeBSD operating system, leveraging the full capabilities of GNU Compiler Collection.

###Video: https://youtu.be/odZNn2lxV-o 

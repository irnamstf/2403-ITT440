`MUHAMMAD HAFIZ BIN JOHARI | 2022883022 | M3CS2554A | ITT440`
# Child Process Termination
## What is Child Process?
<p align="center">
    <img src="https://www.tutorialspoint.com/inter_process_communication/images/system_call.jpg" alt="drawing" width="500"/>
</p>
A child process, in the context of computer science and operating systems, is a process that is created by another process, known as the parent process. When a parent process spawns a child process, the child process typically inherits certain attributes from its parent, such as its memory space, file descriptors, and other resources.

Child processes are commonly used in multitasking operating systems to perform concurrent or parallel tasks. They allow for the delegation of work to separate processes, which can enhance efficiency and scalability in software systems.

In many operating systems, including Unix-like systems such as Linux, child processes are created using system calls like `fork()` or `spawn()`, and they can communicate with their parent process and other processes using inter-process communication mechanisms such as pipes, shared memory, or sockets. Once a child process completes its task, it typically exits and may return a status code to its parent process.


## How to create and terminate child process 

### Step 1: `fork()` System Call
```C
pid_t pid;
pid = fork();
```
The `fork()` system call creates a new process by duplicating the current process. The new process is called the child process, and the original process is called the parent process. The `fork()` system call returns the process ID (PID) of the child process to the parent process, and 0 to the child process.

### Step 2: Error handling
```C
if (pid == -1) {
    printf("Error creating process\n");
    return 1;
}
```
If the `fork()` system call returns -1, it means an error occurred while creating the child process. In this case, the program prints an error message and returns 1 to indicate an error.

### Step 3: Child process termination
```C
if (pid == 0) {
    printf("Child: I'm the child, my internal pid is %d.\n", getpid());
    sleep(1); // Sleep 1 second.
    printf("Child: Done!\n");
}
```
If the `fork()` system call returns 0, it means we are in the child process. 
The child process:
* Prints a message indicating it's the child process, along with its internal PID using `getpid()`.
* Sleeps for 1 second using `sleep(1)`.
* Prints a message indicating it's done.

### Full Code
```C
#include <stdio.h>
#include <signal.h>
#include <unistd.h>

int main() {
    pid_t pid;

    pid = fork();

    if (pid == -1) {
        printf("Error creating process\n");
        return 1;
    }

    if (pid == 0) {
        printf("Child: I'm the child, my internal pid is %d.\n", getpid());
        sleep(1); // Sleep 1 second.
        printf("Child: Done!\n");
    } else {
        printf("Parent: I'm the parent, my child's pid is %d.\n", pid);
        kill(pid, SIGTERM); // Send SIGTERM signal to child process
        printf("Parent: Done!\n");
    }

    return 0;
}

```

### Output

Command to compile and execute:
```gcc
$ gcc saimensirshadan.c -o saimensirshadan
$ ./saimensirshadan
```

Example output:
```gcc
Parent: I'm the parent, my child's pid is 1234
Child: I'm the child, my internal pid is 1234.
Child: Done!
Parent: My child exited with status 42
Parent: My child's exit code is 42
```

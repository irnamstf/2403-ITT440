`MUHAMMAD HAFIZ BIN JOHARI | 2022883022 | M3CS2554A | ITT440`
# Child Process Termination
## What is Child Process?
A child process, in the context of computer science and operating systems, is a process that is created by another process, known as the parent process. When a parent process spawns a child process, the child process typically inherits certain attributes from its parent, such as its memory space, file descriptors, and other resources.

Child processes are commonly used in multitasking operating systems to perform concurrent or parallel tasks. They allow for the delegation of work to separate processes, which can enhance efficiency and scalability in software systems.

In many operating systems, including Unix-like systems such as Linux, child processes are created using system calls like `fork()` or `spawn()`, and they can communicate with their parent process and other processes using inter-process communication mechanisms such as pipes, shared memory, or sockets. Once a child process completes its task, it typically exits and may return a status code to its parent process.

## Process Overview
### Fork() - System Call
<p align="center">
    <img src="https://www.tutorialspoint.com/inter_process_communication/images/system_call.jpg" alt="drawing" width="500"/>
</p>

System call `fork()` is used to create processes. It takes no arguments and returns a process ID. The purpose of `fork()` is to create a new process, which becomes the child process of the caller. After a new child process is created, both processes will execute the next instruction following the `fork()` system call. Therefore, we have to distinguish the parent from the child. This can be done by testing the returned value of `fork()`:

- If `fork()` returns a negative value, the creation of a child process was unsuccessful.
- `fork()` returns a zero to the newly created child process.
- `fork()` returns a positive value, the process ID of the child process, to the parent. The returned process ID is of type `pid_t` defined in sys/types.h. Normally, the process ID is an integer. Moreover, a process can use function `getpid()` to retrieve the process ID assigned to this process.

Therefore, after the system call to `fork()`, a simple test can tell which process is the child. Please note that Unix will make an exact copy of the parent's address space and give it to the child. Therefore, the parent and child processes have separate address spaces.

### Process Creation
- When a new process is created, the operating system assigns a unique Process Identifier (PID) to it.
- The operating system allocates memory space for the process, including program code, data, and stack.
- The Process Control Block (PCB) is initialized with relevant information, such as the process ID, parent’s PID, and other details.
- The process is linked to the scheduling queue and transitions from the “New” state to the “Ready” state, where it competes for CPU time.
- Additional data structures, like log files or accounting files, are created to track process activity.

### Process Termination
A process can terminate in two ways:
- Self-termination: When a process finishes executing its last statement, it naturally terminates. The operating system uses the exit() system call to delete its context.
- Parent-initiated termination: A parent process may terminate its child process for reasons such as, `1` The task assigned to the child is no longer needed. `2` The child has exceeded its resource limits. `3` The parent process itself is exiting, leading to cascaded termination of all its children


## ITT440 Individual Assignment 10%
### Name: Farina Athirah binti Roslee
### Student ID: 2022214142
### Group: M3CS2554A
### Lecturer's Name: Sir Shahadan Saad

# SIGTERM
## Introduction to Signal
- A signal can be defined as a software interrupt or a notification that alerts a process about an event occurring in the system.
- Signals offer a versatile mechanism for efficient event handling and coordination between processes, enhancing the overall functionality and reliability of C programs.
- In other words, signal serve as a mean of communication between a running program (process) and the operating system, allowing the program to respond to various events in an unsynchronized manner.
- There are a few signal functions that can be used and each function has its own usage, such as kill() or raise() functions.

## What is SIGTERM?
- SIGTERM signal is used for **terminating a program**. The SIGTERM can also be referred as a soft kill because the process that receives the SIGTERM signal may choose to ignore it.
- Unlike SIGGKILL, this signal can be blocked, handled and ignored. The shell command 'kill' generates 'SIGTERM' by default.

### How to Send SIGTERM?
- To send SIGTERM signal in C, we can use kill() function. Remember that SIGTERM allows the process to clean up and exit gracefully. It is much mire better to use SIGTERM first and only use SIGKILL for last resort.

## C Program for SIGTERM
```C
#include <signal.h>
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <unistd.h>

void sigterm();
void main(){

        int pid;
        pid = fork();   //get child process

        if (pid < 0){

                perror ("fork");
                exit(1);
        }

        if (pid = 0){

                signal(SIGTERM, sigterm);
                for (int x = 1;; x++);
        }

        else {          //parent

                printf("\nPARENT: sending SIGTERM\n\n");
                kill (pid, SIGTERM);
                sleep(1);       //pause for 1 second
        }
}
void sigterm(){

        signal(SIGTERM, sigterm);
        printf("CHILD: I have received SIGTERM\n");
}
```
## Sample Output
![ss ](https://github.com/addff/2403-ITT440/assets/166006878/5fb26bf7-182a-4f5d-8c81-dcd761d948d0)

## Youtube Link
- This is the youtube link for further explanation regarding SIGTERM in C
- 

## References
- [Termination Signals] (https://www.gnu.org/software/libc/manual/html_node/Termination-Signals.html#:~:text=The%20SIGTERM%20signal%20is%20a,kill%20generates%20SIGTERM%20by%20default.)
- 

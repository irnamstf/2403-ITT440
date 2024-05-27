`Name: Afiq Irfan bin Norfizwan` `Student ID: 2022453266` `Group: M3CS2554A` `Lecturer's Name: Sir Shahadan Saad`
# INDIVIDUAL ASSIGNMENT 10% 
## INTRODUCTION TO SIGNAL
- A signal is a **software generated interrupt** that is sent to a process by the OS because of when user press ctrl-c or another process tell something to this process.
There are fix set of signals that can be sent to a process. Signal are identified by integers. 
- It is asynchronously sent to a running program to notify it of some event. The system interrupts the process’ normal execution to trigger a specific reaction like, among other things, terminating it. Hence, signals are a sort of **inter-process communication**.

## HANDLING SIGHUP IN C
- The SIGHUP (“hang-up”) signal is used to **report that the user’s terminal is disconnected**.
- This signal is also used to report the termination of the controlling process on a terminal to jobs associated with that session, where the termination effectively disconnects all processes in the session from the controlling terminal.
- SIGHUP is commonly used to instruct deamon processes to reload the configuration files **without restarting it**. 
- The signal can be sent manually using function such as `kill()` or `raise()`. The standard library provides functions such as `signal()` to register signal handlers. This function defines the actione need to be taken when the signal is received.

## SAMPLE OUTPUT
````C
#include <signal.h>
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <unistd.h>

void sighup();

void main(){
    int pid;
    pid = fork();

    if (pid < 0){
        perror ("fork");
        exit (1);
    }

    if (pid = 0){
        signal (SIGHUP, sighup);
        for (int x = 1;; x++);
    }

    else {
        printf("\nPARENT: sending SIGHUP\n\n");
        kill(pid, SIGHUP);
        sleep(1);    //pause for 1 second
    }
}

void sighup(){
    signal (SIGHUP, sighup);
    printf ("CHILD: I have received SIGHUP\n");
}
````
## SAMPLE OUTPUT

![ss2](https://github.com/addff/2403-ITT440/assets/166041339/af16fd7c-facd-42cd-a56a-2adac184b671)

## YOUTUBE LINK

## REFERENCES
- [Signals in C Language](https://www.geeksforgeeks.org/signals-c-language/)
- [Sending and Intercepting a Signal in C](https://www.codequoi.com/en/sending-and-intercepting-a-signal-in-c/)
- [Termination Signals](https://www.gnu.org/software/libc/manual/html_node/Termination-Signals.html#:~:text=The%20SIGHUP%20(%E2%80%9Chang%2Dup,or%20telephone%20connection%20was%20broken))

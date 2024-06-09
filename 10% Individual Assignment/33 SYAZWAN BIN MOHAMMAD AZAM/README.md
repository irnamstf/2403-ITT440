`SYAZWAN BIN MOHAMMAD AZAM | 2022867954 | M3CS2554A | ITT440`
# SIGKILL

## What is SIGKILL?
SIGKILL is a signal which is a method of communication between multiple process. It is commonly used in Unix or Unix-Like operating systems like Linux as a way to immediately terminate a process. A signal are send to a running program as a message to triggers a specific action (terminating or handling error). It a type of Inter Process Communication (IPC) which involves the operating system sending signals to target processes while waiting for instruction to complete, interrupting process execution, and handling the signal.

## Function of SIGKILL 
SIGKILL give command to the process to terminate immediately. This command cannot be ignored or blocked and once the process was killed while it is running threads, those will be killed as well. If the process and its threads cannot be terminated by SIGKILL, this indicates an operating system malfunction

## When SIGKILL Should Be Use
Signal SIGKILL should not be use for programs that are complex and only be use on simple program as it can be corrupt during the termination process if it hasn’t completed its cleanup. SIGKILL should only be use on the following situation :
* A bug or error occur in the process during its cleanup
* To retain data for troubleshooting
* Suspicious malware in the process

## How To Send Signal SIGKILL
The code must include `<signal.h>` library for handling signal. `signal(SIGKILL, sigkill);` need to be declared in order to send signal SIGKILL. To send a signal SIGKILL to a process is `kill(pid, SIGKILL);`.

```c
#include <signal.h>
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <unistd.h>

void sigkill();
int main()
{
  int pid;                                        //get child process
  pid = fork();
  
  if (pid<0)
  {
    perror("fork");
    exit(1);
  }
  if (pid=0)                                      //child
  {  
    signal(SIGKILL, sigkill);
    for (int x =1;; x++);
  }
  else                                            //parent
  {
    printf("\nPARENT: sending SIGKILL\n\n");
    kill(pid, SIGKILL);
    sleep(1);                                     //pause for 1 sec
  }
}
void sigkill()
{
  signal(SIGKILL, sigkill);
  printf("CHILD: I have received a SIGKILL\n");
}

```
## Output
![image](https://github.com/addff/2403-ITT440/assets/166005094/c15c7277-bb66-4686-aeb3-5d324e4836cd)


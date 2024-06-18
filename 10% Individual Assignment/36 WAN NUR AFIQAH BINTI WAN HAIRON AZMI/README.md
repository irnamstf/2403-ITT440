**ITT440 - ASSIGNMENT INDIVIDUAL**

**TOPIC – HOW TO COMPILE FORK PROGRAM IN C**

**WAN NUR AFIQAH BINTI WAN HAIRON AZMI**

**2022484148**


# FORK( )

Fork system call is used for creating a new process, which is called child process, 
which runs concurrently with the process that makes the fork( ) call (parent process). 
After a new child process is created, both processes will execute the next instruction 
following the fork( ) system call. A child process uses the same pc (program counter), 
same CPU registers, same open files which use in the parent process. It takes no 
parameters and returns an integer value.

# OVERVIEW
- Involve 2 kind of process which are child process and parent process. 
- Child process run concurrently with the process that make the fork( ) call which is the parent process. 
- Parameters;-
    - Negative value (-1)
  
      - Creation of a child process was unsuccessful.
  
    - Zero (0)
  
      - Returned to the newly created child process.
  
    - Positive value (+1)
   
      - Return to the newly created child process.
  
- The fork( ) system call is used for creating a new process by duplicating the existing process, resulting in two processes running at the same time.
- If we call fork( ) twice, it will spawn 2(2) = 4 processes. The formula is 2n, whereas n is equal to number of fork( ) command. Which mean if the amount of fork in the command (n) is 3, resulting the output into 8

# HOW TO COMPILE FORK( ) IN C
**STEP 1:** Use the command `` pkg install gcc `` to install the C language compiler. Then, use the command `` pkg install tree `` to install the tree.

**STEP 2:** create a folder by using command `` mkdir ‘name of the folder’ `` for example `` mkdir WEEK01 `` and to attach file c within the folder use command `` touch ‘name of the file’ ``, for example `` touch WEEK01/hello.c ``.

![2](https://github.com/addff/2403-ITT440/assets/166004641/9faaa45d-2393-48c0-a5ff-a3e749054d2e)

**STEP 3:** to enter the editor of the file, use command ``ee ‘file name’``, for example ``ee ./WEEK01/hello.c``

![3](https://github.com/addff/2403-ITT440/assets/166004641/5315c7e0-23a9-45b4-a4f6-ce3940580904)

**STEP 4:** enter the coding
```
#include <stdio.h>
#include <unistd.h>
#include <sys/wait.h>
#include <stdlib.h>

int main()
{
        pid_t child_pid;
        int child_status;
        child_pid = fork();

        switch (child_pid)
        {
                case -1:
                  perror("fork");
                  exit(1);                        //fork() successed, child process

                case 0:                          
                  printf("Hello World!\n");
                  exit(0);                        //child process exit
                       
                default:                          //fork() successed, parent process
                  wait(&child_status);            //wait untill child process exit
        }
        return 0;
}
```

**STEP 5:** to compile the coding, use ``gcc ‘file name’``, for example ``gcc ./WEEK01/hello.c`` 

![4](https://github.com/addff/2403-ITT440/assets/166004641/6b206053-2650-43e6-be47-5a15ad6562b4)

**STEP 6:** use command ``./a.out`` to display the output

![1](https://github.com/addff/2403-ITT440/assets/166004641/80c08c13-757b-42b8-acb2-7a63459d4eac)

## EXAMPLE 1

**n=1, 2<sup>1</sup>**

```
#include <stdio.h>
#include <unistd.h>
#include <sys/wait.h>
#include <stdlib.h>

int main()
{
        pid_t child_pid;
        int child_status;
        child_pid = fork();

        switch (child_pid)
        {
                case -1:
                  perror("fork");
                  exit(1);                        //fork() successed, child process

                case 0:
                  fork( );                        // fork                          
                  printf("Hello World!\n");
                  exit(0);                        //child process exit
                       
                default:                          //fork() successed, parent process
                  wait(&child_status);            //wait untill child process exit
        }
        return 0;
}
```
**OUTPUT -->**

![5](https://github.com/addff/2403-ITT440/assets/166004641/a40c397d-fc01-4971-882c-496544699f7d)

## EXAMPLE 2

**n=2, 2<sup>2</sup>**

```
#include <stdio.h>
#include <unistd.h>
#include <sys/wait.h>
#include <stdlib.h>

int main()
{
        pid_t child_pid;
        int child_status;
        child_pid = fork();

        switch (child_pid)
        {
                case -1:
                  perror("fork");
                  exit(1);                        //fork() successed, child process

                case 0:
                  fork( );                        // fork 
                  fork( );                                               
                  printf("Hello World!\n");
                  exit(0);                        //child process exit
                       
                default:                          //fork() successed, parent process
                  wait(&child_status);            //wait untill child process exit
        }
        return 0;
}
```
**OUTPUT -->**

![6](https://github.com/addff/2403-ITT440/assets/166004641/f4a2a342-7a5a-4e70-a0dd-9b9816ca6f51)

### Video: https://www.youtube.com/watch?v=1-Jau7I6Gdk

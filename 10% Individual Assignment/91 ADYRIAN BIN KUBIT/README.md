TITLE: PIPE() SYSTEM CALL

NAME: ADYRIAN BIN KUBIT

STUDENT ID: 2021853946

GROUP: M3CS2554A

LECTURER'S NAME: SIR SHAHADAN BIN SAAD


PIPE() SYSTEM CALL
------------------

Pipe() system call is a communication mechanisms via pipes. this system creates a pipe that will be used to communicate with a process we'll fork off to. 

pipe() system call is one of the communication mechanisms that exists in network programming. this system creates a pipe that is used for communication with a forked process.

Pipe() system call is taken as an argument of an array of 2 integers that is used to save two file descriptors used to access the pipe:
 - first, to read on the pipe
 - second, to write on the pipe

below is a commented program that explains and demonstrate the usage of pipe() for parent process to send a message to child process through a pipe. 

    #include <stdio.h>
    #include <stdlib.h>
    #include <uinstd.h>
    #include <string.h>

    int main(void) {
      int pipefd[2];
      pid_t cpid;
      char buf;
      char message[] = "Hello from parent";

                                                       //create a pipe
    if (pipe(pipefd) == -1) {
        perror("pipe");
        exit(EXIT_FAILURE);
    }

                                                       // Fork a child process
    cpid = fork();
    if (cpid == -1) {
        perror("fork");
        exit(EXIT_FAILURE);
    }

    if (cpid == 0) {                                   // Child process
        close(pipefd[1]);                              // Close unused write end

        printf("Child received: ");
                                                       // Read from the pipe and print the received message
        while (read(pipefd[0], &buf, 1) > 0) {
            write(STDOUT_FILENO, &buf, 1);
        }
        printf("\n");

        close(pipefd[0]);                              // Close read end
        _exit(EXIT_SUCCESS);

    }
      else {                                           // Parent process
        close(pipefd[0]);                              // Close unused read end

                                                       // Write the message to the pipe
        write(pipefd[1], message, strlen(message));
        close(pipefd[1]);                              // Close write end, causing EOF in the child

        wait(NULL);  // Wait for child to finish
        exit(EXIT_SUCCESS);
      }
    }
    

below is the expected output for a successful run of this program.
```
Child received: Hello from parent
```

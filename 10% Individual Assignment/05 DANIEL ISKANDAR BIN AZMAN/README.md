` DANIEL ISKANDAR BIN AZMAN | 2022850768 | M3CS2554A | ITT440 `
# HOW TO SEND AND RECEIVE UDP PACKET USING C
## INTRODUCTION OF C
C is a general-purpose, procedural programming language that has been widely used for developing system and application software. It was originally developed by Dennis Ritchie between 1969 and 1973 at Bell Labs, and it has since become one of the most influential programming languages, forming the basis for many modern languages, such as C++, C#, and Objective-C.
## IMPORTANCE OF C
- Foundation of Modern Languages: C has influenced many modern programming languages, making its concepts and syntax familiar to many developers.
- System Programming: C is extensively used for developing operating systems, embedded systems, and other low-level software where direct hardware manipulation is required.
- Performance: C is known for its performance and efficiency, making it ideal for applications that require high-speed computations and resource management.
- Educational Value: Learning C provides a solid foundation in programming and understanding how software interacts with hardware, which is essential for computer science education.
## SEND UDP PACKET IN UDP CLIENT
-Socket Creation: socket(AF_INET, SOCK_DGRAM, 0) creates a UDP socket.

-Server Address Setup: The server_addr structure is set with the server's IP address and port.

-Send Message: sendto sends the message to the server.

-Receive Response: recvfrom waits for the server's response.

-Print Response: The server's response is printed to the console.

-Close Socket: close(sockfd) closes the socket.

## CODING
````C
// udp_client.c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <arpa/inet.h>

#define SERVER_PORT 8080
#define BUFFER_SIZE 1024

int main() {
    int sockfd;
    struct sockaddr_in server_addr;
    char *message = "Hello, UDP Server!";
    char buffer[BUFFER_SIZE];
    socklen_t addr_len = sizeof(server_addr);

    // Create UDP socket
    if ((sockfd = socket(AF_INET, SOCK_DGRAM, 0)) < 0) {
        perror("socket creation failed");
        exit(EXIT_FAILURE);
    }

    // Server information
    memset(&server_addr, 0, sizeof(server_addr));
    server_addr.sin_family = AF_INET;
    server_addr.sin_port = htons(SERVER_PORT);
    server_addr.sin_addr.s_addr = inet_addr("127.0.0.1"); // Server's IP address

    // Send message to server
    if (sendto(sockfd, message, strlen(message), 0, (const struct sockaddr *)&server_addr, addr_len) < 0) {
        perror("sendto failed");
        close(sockfd);
        exit(EXIT_FAILURE);
    }

    printf("Message sent to server.\n");

    // Receive response from server
    int n = recvfrom(sockfd, buffer, BUFFER_SIZE, 0, (struct sockaddr *)&server_addr, &addr_len);
    if (n < 0) {
        perror("recvfrom failed");
        close(sockfd);
        exit(EXIT_FAILURE);
    }

    buffer[n] = '\0';
    printf("Server response: %s\n", buffer);

    // Close the socket
    close(sockfd);
    return 0;
}

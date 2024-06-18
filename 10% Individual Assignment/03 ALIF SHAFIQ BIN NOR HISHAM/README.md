**Student Name** : ALIF SHAFIQ BIN NOR HISHAM

**Student ID**   : 2022862154

**Group**        : M3CS2554A

**Tittle**       : ITT440 10% Individual Assignment 

**Lecturer**     : Sir Shahadan Saad

# TCP VS UDP in C

## What is TCP ?

### Definition

TCP (Transmission Control Protocol) is one of the main protocols in the Internet Protocol Suite, often referred to as TCP/IP. It operates at the transport layer of the OSI model and provides reliable, connection-oriented communication between devices over an IP network.

### What is UDP ?

UDP (User Datagram Protocol) is another transport layer protocol in the Internet Protocol Suite, just like TCP. However, unlike TCP, UDP is connectionless and provides unreliable, best-effort delivery of data packets between devices over an IP network.

_The diagram show how the `UDP and TCP` work_ :

![tcp-udp-2](https://github.com/alepJames/AlepProject/assets/168588890/b510a1c4-41f1-4913-b023-81f74f7afb86)

## What is Difference Between TCP And UDP Coding in C
### TCP :
* `Connection-oriented`: A connection is established before data is sent.
* `Reliable`: TCP ensures that data is delivered in the correct order and retransmits lost or corrupted packets.
* `Error-checked`: TCP performs error-checking on data packets to ensure integrity.
* `Flow control`: TCP regulates the amount of data that can be sent at one time to prevent network congestion.
* `Multiplexing`: TCP allows multiple applications to share the same connection.

### UDP :
* `Connection-oriented`: No connection is established before data is sent.
* `Best-effort delivery`: UDP does not guarantee delivery or order of packets.
* `Error-tolerant`: UDP does not perform error-checking on data packets.
* `Fast transmission`: UDP is generally faster than TCP due to lower overhead.
* `No flow control`: UDP does not regulate the amount of data sent.

# Here are the step by step for coding for TCP And UDP that use c as the programming language
## Step by step TCP coding for Server
### Step 1 : Include necessary headers
The code start by including the necessary headers:
```C
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
```

These headers provide the necessary functions and data types for working with sockets, networking, and input/output operations.

### Step 2 : Define Constant
The code defines two constants:
```C
#define PORT 8080
#define BUFFER_SIZE 1024
```
`PORT` is set to 8080, which is the port number that the server will listen on. `BUFFER_SIZE` is set to 1024, which is the size of the buffer used to store incoming data.

### Step 3 : Create a socket 
The code creates a socket using the `socket` function:
```C
if ((server_fd = socket(AF_INET, SOCK_STREAM, 0)) == 0) {
    perror("socket failed");
    exit(EXIT_FAILURE);
}
```
The `socket` function takes three arguments: `AF_INET` specifies the address family (IPv4), `SOCK_STREAM` specifies the socket type (stream-oriented), and `0` specifies the protocol (TCP). The function returns a file descriptor for the socket, which is stored in `server_fd`. If the socket creation fails, the code prints an error message and exits.

### Step 4 : Set socket options 
The code sets socket options using the `setsockopt` function:
```C
if (setsockopt(server_fd, SOL_SOCKET, SO_REUSEADDR | SO_REUSEPORT, &opt, sizeof(opt))) {
    perror("setsockopt");
    exit(EXIT_FAILURE);
}
```
The `setsockopt` function takes five arguments: `server_fd` is the socket file descriptor, `SOL_SOCKET` specifies the socket level, `SO_REUSEADDR | SO_REUSEPORT` specifies the options to set, `&opt` is a pointer to an integer that specifies the value of the options, and sizeof(opt) specifies the size of the option value. The options `SO_REUSEADDR` and `SO_REUSEPORT` allow the socket to reuse the address and port even if they are already in use.

### Step 5 : Fill server address 
The code fills in the server address using the `struct sockaddr_in` structure:
```C
address.sin_family = AF_INET;
address.sin_addr.s_addr = INADDR_ANY;
address.sin_port = htons(PORT);
```
The `struct sockaddr_in` structure is used to represent an IPv4 address. The `sin_family` field is set to `AF_INET` to specify the address family. The `sin_addr.s_addr` field is set to `INADDR_ANY` to specify that the server should listen on all available network interfaces. The `sin_port` field is set to `htons(PORT)` to specify the port number.

### Step 6 : Bind socket address 
The code binds the socket to the server address using the `bind` function:
```C
if (bind(server_fd, (struct sockaddr *)&address, sizeof(address))<0) {
    perror("bind failed");
    exit(EXIT_FAILURE);
}
```
The `bind` function takes three arguments: `server_fd` is the socket file descriptor, `(struct sockaddr *)&address` is the server address, and `sizeof(address)` specifies the size of the server address. The function binds the socket to the server address. If the binding fails, the code prints an error message and exits.

### Step 7 : Listen for incoming connections
The code listens for incoming connections using the `listen` function:
```C
if (listen(server_fd, 3) < 0) {
    perror("listen");
    exit(EXIT_FAILURE);
}
```
The `listen` function takes two arguments: `server_fd` is the socket file descriptor, and `3` specifies the maximum number of pending connections. If the listening fails, the code prints an error message and exits.

### Step 8 : Accept incoming connection
The code accepts an incoming connection using the `accept` function:
```C
if ((new_socket = accept(server_fd, (struct sockaddr *)&address, (socklen_t*)&addrlen))<0) {
    perror("accept");
    exit(EXIT_FAILURE);
}
```
### Step 9 : Read the data from the client 
The code reads data from the client using the `read` function:
```C
valread = read(new_socket, buffer,
```

##  Full TCP coding for Server 



```C
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>

#define PORT 8080
#define BUFFER_SIZE 1024

int main() {
    int server_fd, new_socket, valread;
    struct sockaddr_in address;
    int opt = 1;
    int addrlen = sizeof(address);
    char buffer[BUFFER_SIZE] = {0};
    char *hello = "Hello from server";

    // Creating socket file descriptor
    if ((server_fd = socket(AF_INET, SOCK_STREAM, 0)) == 0) {
        perror("socket failed");
        exit(EXIT_FAILURE);
    }

    // Forcefully attaching socket to the port 8080
    if (setsockopt(server_fd, SOL_SOCKET, SO_REUSEADDR | SO_REUSEPORT, &opt, sizeof(opt))) {
        perror("setsockopt");
        exit(EXIT_FAILURE);
    }
    address.sin_family = AF_INET;
    address.sin_addr.s_addr = INADDR_ANY;
    address.sin_port = htons(PORT);

    // Forcefully attaching socket to the port 8080
    if (bind(server_fd, (struct sockaddr *)&address, sizeof(address))<0) {
        perror("bind failed");
        exit(EXIT_FAILURE);
    }
    if (listen(server_fd, 3) < 0) {
        perror("listen");
        exit(EXIT_FAILURE);
    }
    if ((new_socket = accept(server_fd, (struct sockaddr *)&address, (socklen_t*)&addrlen))<0) {
        perror("accept");
        exit(EXIT_FAILURE);
    }
    valread = read(new_socket, buffer, BUFFER_SIZE);
    printf("%s\n",buffer);
    send(new_socket, hello, strlen(hello), 0);
    printf("Hello message sent\n");
    return 0;
}
```
### Compiling :

```C
gcc server.c -o server
```
### Output:

```C
$ ./server
Hello from client
```
## Step by step TCP coding for Client

### Step 1: Include necessary headers
The code starts by including the necessary headers:
```C
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <netdb.h>
```
These headers provide the necessary functions and data types for working with sockets, networking, and input/output operations.

### Step 2: Define constants
The code defines two constants:
```C
#define PORT 8080
#define BUFFER_SIZE 1024
```
`PORT` is set to 8080, which is the port number that the client will connect to. `BUFFER_SIZE` is set to 1024, which is the size of the buffer used to store incoming data.

### Step 3: Create a socket
The code creates a socket using the `socket` function:
```C
if ((sock = socket(AF_INET, SOCK_STREAM, 0)) < 0) {
    printf("\n Socket creation error \n");
    return -1;
}
```
The `socket` function takes three arguments: `AF_INET` specifies the address family (IPv4), `SOCK_STREAM` specifies the socket type (stream-oriented), and `0` specifies the protocol (TCP). The function returns a file descriptor for the socket, which is stored in `sock`. If the socket creation fails, the code prints an error message and returns -1.
### Step 4: Fill server address
The code fills in the server address using the `struct sockaddr_in` structure:
```C
serv_addr.sin_family = AF_INET;
serv_addr.sin_port = htons(PORT);
```
The `struct sockaddr_in` structure is used to represent an IPv4 address. The `sin_family` field is set to `AF_INET` to specify the address family. The `sin_port` field is set to `htons(PORT)` to specify the port number.

### Step 5: Convert IP address to binary form
The code converts the IP address "127.0.0.1" to binary form using the `inet_pton` function:
```C
if(inet_pton(AF_INET, "127.0.0.1", &serv_addr.sin_addr)<=0) {
    printf("\nInvalid address/ Address not supported \n");
    return -1;
}
```
The `inet_pton` function takes three arguments: `AF_INET` specifies the address family, `"127.0.0.1"` is the IP address to convert, and `&serv_addr.sin_addr` is the buffer to store the binary form of the address. If the conversion fails, the code prints an error message and returns -1.

### Step 6: Connect to server
The code connects to the server using the connect function:
```C
if (connect(sock, (struct sockaddr *)&serv_addr, sizeof(serv_addr)) < 0) {
    printf("\nConnection Failed \n");
    return -1;
}
```
The `connect` function takes three arguments: `sock` is the socket file descriptor, `(struct sockaddr *)&serv_addr` is the server address, and `sizeof(serv_addr)` specifies the size of the server address. If the connection fails, the code prints an error message and returns -1.

### Step 7: Send data to server
The code sends data to the server using the `send` function:
```C
send(sock, hello, strlen(hello), 0);
printf("Hello message sent\n");
```
The `send` function takes four arguments: `sock` is the socket file descriptor, `hello` is the data to send, `strlen(hello)` is the length of the data, and `0` specifies the flags. The function sends the data to the server and prints a success message.

### Step 8: Receive data from server
The code receives data from the server using the read function:
```C
valread = read(sock, buffer, BUFFER_SIZE);
printf("%s\n",buffer);
```
The `read` function takes three arguments: `sock` is the socket file descriptor, `buffer` is the buffer to store the incoming data, and `BUFFER_SIZE` specifies the size of the buffer. The function reads data from the server and stores it in the buffer. The buffer is then printed to the console.

##  Full TCP coding for Server 
```C
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <netdb.h>

#define PORT 8080
#define BUFFER_SIZE 1024

int main(int argc, char const *argv[]) {
    int sock = 0, valread;
    struct sockaddr_in serv_addr;
    char *hello = "Hello from client";
    char buffer[BUFFER_SIZE] = {0};

    if ((sock = socket(AF_INET, SOCK_STREAM, 0)) < 0) {
        printf("\n Socket creation error \n");
        return -1;
    }

    serv_addr.sin_family = AF_INET;
    serv_addr.sin_port = htons(PORT);

    // Convert IPv4 and IPv6 addresses from text to binary form
    if(inet_pton(AF_INET, "127.0.0.1", &serv_addr.sin_addr)<=0) {
        printf("\nInvalid address/ Address not supported \n");
        return -1;
    }

    if (connect(sock, (struct sockaddr *)&serv_addr, sizeof(serv_addr)) < 0) {
        printf("\nConnection Failed \n");
        return -1;
    }

    send(sock, hello, strlen(hello), 0);
    printf("Hello message sent\n");
    valread = read(sock, buffer, BUFFER_SIZE);
    printf("%s\n",buffer);
    return 0;
}
```

### Compiling :

```C
gcc client.c -o client
```

### Output

```C
$ ./client
Hello message sent
Hello from server
```
* This output demonstrates the communication between the client and server. The client sends "Hello from client" to the server, and the server responds with "Hello from server".


## Step By Step UDP coding for Server
### Step 1 : Include necessary headers
The code starts by including the necessary headers:
```C
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <arpa/inet.h>
```
These headers provide the necessary functions and data types for working with sockets, networking, and input/output operations.
### Step 2: Define constants
The code defines two constants:
```C
#define PORT 8080
#define BUFFER_SIZE 1024
```
`PORT` is set to 8080, which is the port number that the server will listen on. `BUFFER_SIZE` is set to 1024, which is the size of the buffer used to store incoming data.

### Step 3: Create a socket
The code creates a socket using the socket function:
```C
if ((sockfd = socket(AF_INET, SOCK_DGRAM, 0)) < 0) {
    perror("socket creation failed");
    exit(EXIT_FAILURE);
}
```
The `socket` function takes three arguments: `AF_INET` specifies the address family (IPv4), `SOCK_DGRAM` specifies the socket type (datagram-oriented), and `0` specifies the protocol (UDP). The function returns a file descriptor for the socket, which is stored in `sockfd`. If the socket creation fails, the code prints an error message and exits.
### Step 4: Initialize server and client addresses
The code initializes the server and client addresses using the `memset` function:
```C
memset(&servaddr, 0, sizeof(servaddr));
memset(&cliaddr, 0, sizeof(cliaddr));
```
The `memset` function sets the memory region pointed to by `servaddr` and `cliaddr` to zero.

### Step 5: Fill server information
The code fills in the server information using the `struct sockaddr_in` structure:
```C
servaddr.sin_family = AF_INET; // IPv4
servaddr.sin_addr.s_addr = INADDR_ANY;
servaddr.sin_port = htons(PORT);
```
The `struct sockaddr_in` structure is used to represent an IPv4 address. The `sin_family` field is set to `AF_INET` to specify the address family. The `sin_addr.s_addr` field is set to `INADDR_ANY` to specify that the server should listen on all available network interfaces. The `sin_port` field is set to `htons(PORT)` to specify the port number.

### Step 6: Bind the socket with the server address
The code binds the socket with the server address using the `bind` function:
```C
if (bind(sockfd, (const struct sockaddr *)&servaddr, sizeof(servaddr)) < 0) {
    perror("bind failed");
    exit(EXIT_FAILURE);
}
```
The `bind` function takes three arguments: `sockfd` is the socket file descriptor, `(const struct sockaddr *)&servaddr` is the server address, and `sizeof(servaddr)` specifies the size of the server address. The function binds the socket to the server address. If the binding fails, the code prints an error message and exits.

### Step 7: Receive data from client
The code receives data from the client using the `recvfrom` function:
```C
len = sizeof(cliaddr); //len is value/resuslt

n = recvfrom(sockfd, (char *)buffer, BUFFER_SIZE, MSG_WAITALL, (struct sockaddr *)&cliaddr, &len);
buffer[n] = '\0';
printf("Client : %s\n", buffer);
```
The `recvfrom` function takes six arguments: `sockfd` is the socket file descriptor, `(char *)buffer` is the buffer to store the incoming data, `BUFFER_SIZE` is the size of the buffer, `MSG_WAITALL` specifies the message flags, `(struct sockaddr *)&cliaddr` is the client address, and `&len` specifies the size of the client address. The function receives the data from the client and stores it in the buffer. The buffer is then null-terminated and printed to the console.

### Step 8: Send response to client
The code sends a response to the client using the sendto function:
```C
sendto(sockfd, (const char *)"Hello from server", strlen("Hello from server"), MSG_CONFIRM, (const struct sockaddr *)&cliaddr, len);
printf("Hello message sent.\n");
```
The `sendto` function takes six arguments: `sockfd` is the socket file descriptor, `(const char *)"Hello from server"` is the data to be sent, `strlen("Hello from server")` is the length of the data, `MSG_CONFIRM` specifies the message flags, `(const struct sockaddr *)&cliaddr` is the client address, and `len` specifies the size of the client address. The function sends the data to the client and prints a success message.

### Full UDP Coding For Server

```C
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <arpa/inet.h>

#define PORT 8080
#define BUFFER_SIZE 1024

int main() {
    int sockfd;
    char buffer[BUFFER_SIZE];
    struct sockaddr_in servaddr, cliaddr;

    // Creating socket file descriptor
    if ((sockfd = socket(AF_INET, SOCK_DGRAM, 0)) < 0) {
        perror("socket creation failed");
        exit(EXIT_FAILURE);
    }

    memset(&servaddr, 0, sizeof(servaddr));
    memset(&cliaddr, 0, sizeof(cliaddr));

    // Filling server information
    servaddr.sin_family = AF_INET; // IPv4
    servaddr.sin_addr.s_addr = INADDR_ANY;
    servaddr.sin_port = htons(PORT);

    // Bind the socket with the server address
    if (bind(sockfd, (const struct sockaddr *)&servaddr, sizeof(servaddr)) < 0) {
        perror("bind failed");
        exit(EXIT_FAILURE);
    }

    int len, n;

    len = sizeof(cliaddr); //len is value/resuslt

    n = recvfrom(sockfd, (char *)buffer, BUFFER_SIZE, MSG_WAITALL, (struct sockaddr *)&cliaddr, &len);
    buffer[n] = '\0';
    printf("Client : %s\n", buffer);
    sendto(sockfd, (const char *)"Hello from server", strlen("Hello from server"), MSG_CONFIRM, (const struct sockaddr *)&cliaddr, len);
    printf("Hello message sent.\n");

    return 0;
}
```
### Compiling

```C
gcc udp_server.c -o udp_server
```
### Output

```C
$ ./udp_server
Client : Hello from client
Hello message sent.
```

## Step By Step Of UDP Coding For Client
### Step 1: Include necessary headers
The code starts by including the necessary headers:
```C
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <arpa/inet.h>
```
These headers provide the necessary functions and data types for working with sockets, networking, and input/output operations.
### Step 2: Define constants
The code defines two constants:
```C
#define PORT 8080
#define BUFFER_SIZE 1024
```
`PORT` is set to 8080, which is the port number that the client will send data to. `BUFFER_SIZE` is set to 1024, which is the size of the buffer used to store incoming data.

### Step 3: Create a socket
The code creates a socket using the `socket` function:
```C
if ((sockfd = socket(AF_INET, SOCK_DGRAM, 0)) < 0) {
    perror("socket creation failed");
    exit(EXIT_FAILURE);
}
```
The `socket` function takes three arguments: `AF_INET` specifies the address family (IPv4), `SOCK_DGRAM` specifies the socket type (datagram-oriented), and `0` specifies the protocol (UDP). The function returns a file descriptor for the socket, which is stored in `sockfd`. If the socket creation fails, the code prints an error message and exits.

### Step 4: Initialize server address
The code initializes the server address using the `memset` function:
```C
memset(&servaddr, 0, sizeof(servaddr));
```
The `memset` function sets the memory region pointed to by `servaddr` to zero.

### Step 5: Fill server information
The code fills in the server information using the `struct sockaddr_in` structure:
```C
servaddr.sin_family = AF_INET;
servaddr.sin_port = htons(PORT);
servaddr.sin_addr.s_addr = INADDR_ANY;
```
The `struct sockaddr_in` structure is used to represent an IPv4 address. The `sin_family` field is set to `AF_INET` to specify the address family. The `sin_port` field is set to `htons(PORT)` to specify the port number. The `sin_addr.s_addr` field is set to `INADDR_ANY` to specify that the client should send data to any available network interface.
### Step 6: Send data to server
The code sends data to the server using the sendto function:
```C
sendto(sockfd, (const char *)hello, strlen(hello), MSG_CONFIRM, (const struct sockaddr *)&servaddr, sizeof(servaddr));
printf("Hello message sent.\n");
```
The `sendto` function takes six arguments: `sockfd` is the socket file descriptor, `(const char *)`hello is the data to be sent, `strlen(hello)` is the length of the data, `MSG_CONFIRM` specifies the message flags, `(const struct sockaddr *)&servaddr` is the server address, and `sizeof(servaddr)` specifies the size of the server address. The function sends the data to the server and prints a success message.

### Step 7: Receive data from server
The code receives data from the server using the `recvfrom` function:
```C
n = recvfrom(sockfd, (char *)buffer, BUFFER_SIZE, MSG_WAITALL, (struct sockaddr *)&servaddr, &len);
buffer[n] = '\0';
printf("Server : %s\n", buffer);
```
The `recvfrom` function takes six arguments: `sockfd` is the socket file descriptor, `(char *)buffer` is the buffer to store the incoming data, `BUFFER_SIZE` is the size of the buffer, `MSG_WAITALL` specifies the message flags, `(struct sockaddr *)&servaddr` is the server address, and `&len` specifies the size of the server address. The function receives the data from the server and stores it in the buffer. The buffer is then null-terminated and printed to the console.

### Step 8: Close socket
The code closes the socket using the `close` function:
```C
close(sockfd);
```
The `close` function takes one argument: `sockfd` is the socket file descriptor. The function closes the socket and releases any system resources associated with it.

### Full UDP Coding for Client 

```C
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <arpa/inet.h>

#define PORT 8080
#define BUFFER_SIZE 1024

int main() {
    int sockfd;
    char buffer[BUFFER_SIZE];
    char *hello = "Hello from client";
    struct sockaddr_in servaddr;

    // Creating socket file descriptor
    if ((sockfd = socket(AF_INET, SOCK_DGRAM, 0)) < 0) {
        perror("socket creation failed");
        exit(EXIT_FAILURE);
    }

    memset(&servaddr, 0, sizeof(servaddr));

    // Filling server information
    servaddr.sin_family = AF_INET;
    servaddr.sin_port = htons(PORT);
    servaddr.sin_addr.s_addr = INADDR_ANY;

    int n, len;

    sendto(sockfd, (const char *)hello, strlen(hello), MSG_CONFIRM, (const struct sockaddr *)&servaddr, sizeof(servaddr));
    printf("Hello message sent.\n");

    n = recvfrom(sockfd, (char *)buffer, BUFFER_SIZE, MSG_WAITALL, (struct sockaddr *)&servaddr, &len);
    buffer[n] = '\0';
    printf("Server : %s\n", buffer);

    close(sockfd);
    return 0;
}
```

### Compiling

```C
gcc udp_client.c -o udp_client
```

### Output

```C
$ ./udp_client
Hello message sent.
Server : Hello from server
```
* This output demonstrates the communication between the UDP client and server. The client sends "Hello from client" to the server, and the server responds with "Hello from server". Note that UDP is connectionless, so there's no establishment or termination of a connection like in TCP.



## TCP or UDP , Which is better

TCP is better suited for applications that require reliable, ordered transmission of data, while UDP is better for applications that prioritize low latency, minimal overhead, and real-time communication. Ultimately, the choice depends on the specific requirements and constraints of your application.

|TCP  Coding With C | UDP Coding With C |
|-------------------|-------------------|
|High Reliability   |Low Reliability    |
|Lower Speed        |High Speed         |
|Packets are delivered in a sequence|Packets are delivered in a stream|





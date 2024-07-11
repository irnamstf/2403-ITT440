Name: Muhammad Zulfahmie Bin Kelana

No. Matric: 2022615532

Group: M3CDCS2554A

## How to Connect Multiple Vlients to a Server using Python 3 Sockets?

## What is a Client?

A client is the hardware or software that accesses a service on a server. The term "client" may refer to:

- A person using the service
- A piece of software (like a web browser) 
- A hardware device (like a phone or computer)

Clients are the ones that initiate requests for services and resources from the server. They rely on the server to provide the requested information or functionality.

## Types of Clients

There are three main types of clients in a client-server network:

1. **Thick Clients**: Perform most data processing locally and rely on the server only minimally.

2. **Thin Clients**: Rely heavily on the server to handle the bulk of data processing. They have minimal local functionality.

3. **Hybrid Clients**: Combine aspects of both thick and thin clients, doing some local processing but still relying on the server for key functions.

## Client-Server Interaction

In a client-server network, the client sends requests to the server over the network. The server then processes the request and sends a response back to the client. This request-response cycle is the core of how client-server networks operate.

Clients typically connect to servers using the TCP/IP protocol suite, which establishes a reliable connection for the exchange of data packets. The server manages and prioritizes incoming client requests to ensure efficient use of resources.

The key benefit of the client-server model is that it allows clients to access shared resources and services provided by the centralized server, without needing to host all that functionality locally. This makes client-server networks scalable and efficient.

## What is Socket

A socket is a programming interface that provides a way for two or more computers to communicate over a network. It is a low-level interface that allows you to send and receive data over a network using various protocols such as TCP/IP or UDP.

Sockets in Python provide a low-level interface for network programming, allowing you to create client-server applications, chat servers, file transfer utilities, and more. While sockets are powerful, they can be complex to use, especially for building large-scale applications. In such cases, you may want to use higher-level libraries or frameworks that abstract away the socket details.

##There are two main types of sockets:

1. **Stream Sockets (SOCK_STREAM)**: These sockets use the Transmission Control Protocol (TCP) and provide a reliable, connection-oriented, and stream-based communication channel. They ensure that data is delivered in the correct order without any loss or duplication. Examples of stream sockets in Python include:

   - `socket.AF_INET` (IPv4 address family)
   - `socket.AF_INET6` (IPv6 address family)

2. **Datagram Sockets (SOCK_DGRAM)**: These sockets use the User Datagram Protocol (UDP) and provide a connectionless, unreliable, and message-oriented communication channel. Datagrams may arrive out of order, be duplicated, or go missing without any notification. Examples of datagram sockets in Python include:

   - `socket.AF_INET` (IPv4 address family)
   - `socket.AF_INET6` (IPv6 address family)
   - `socket.AF_UNIX` (Unix domain sockets)

The key differences between stream and datagram sockets are:

**Stream Sockets (TCP)**:
- Connection-oriented
- Reliable data transfer
- Ordered delivery of data
- Retransmission of lost data
- Example: HTTP, SMTP, FTP

**Datagram Sockets (UDP)**:
- Connectionless
- Unreliable data transfer
- Unordered delivery of data
- No retransmission of lost data
- Example: DNS, DHCP, video/audio streaming

When creating a socket in Python, you need to specify the socket type using the `socket.SOCK_STREAM` or `socket.SOCK_DGRAM` constants. For example:

```python
import socket

# Create a TCP (stream) socket
tcp_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# Create a UDP (datagram) socket
udp_socket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
```

The choice between stream or datagram sockets depends on the requirements of your application, such as the need for reliability, ordering, or performance.


## Connecting Multiple Clients to a Server

****Establishing the Server****

1. Import the necessary modules:
```python
import socket
import threading
```

2. Create a server socket and bind it to a host and port:
```python
server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server_socket.bind((host, port))
server_socket.listen(5)
```

3. Define a function to handle each client connection in a separate thread:
```python
def handle_client(conn, addr):
    print(f"[NEW CONNECTION] {addr} connected.")

    connected = True
    while connected:
        try:
            message = conn.recv(1024)
            if message == DISCONNECT_MESSAGE:
                connected = False
            print(f"[{addr}] {message}")
            conn.sendall(message)
        except:
            connected = False
            print(f"[{addr}] Disconnected")
            conn.close()

    conn.close()
```

4. Start the server and accept incoming connections, passing each to the `handle_client` function in a new thread:
```python
print("[STARTING] server is starting...")
while True:
    conn, addr = server_socket.accept()
    thread = threading.Thread(target=handle_client, args=(conn, addr))
    thread.start()
    print(f"[ACTIVE CONNECTIONS] {threading.activeCount() - 1}")
```

****Connecting the Clients****

1. Create a client socket and connect to the server:
```python
client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client_socket.connect((host, port))
```

2. Send and receive messages:
```python
message = "Hello, server!"
client_socket.sendall(message.encode())
response = client_socket.recv(1024)
print(f"Received response: {response.decode()}")
```

3. Repeat the above steps for each additional client you want to connect.

The key points are:

- Use a server socket to listen for incoming connections
- Define a function to handle each client connection in a separate thread
- Create a client socket for each client and connect to the server
- Send and receive messages between the clients and server

By using multi-threading, the server can handle multiple clients concurrently, allowing for real-time communication between the clients and server. The provided code demonstrates the basic structure, and you can build upon it to create more complex chat or gaming applications.

## Video

This is one example on How to connect multiple clients to a  server using python 3 sockets 

https://youtu.be/3QiPPX-KeSc?si=Nvowg427Hcm3IpbF

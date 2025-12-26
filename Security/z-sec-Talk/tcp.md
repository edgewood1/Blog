 
)
https://en.wikipedia.org/wiki/Internet_protocol_suite


transmission control protocol

TCP protocol operations may be divided into three phases. Connection establishment is a multi-step handshake process that establishes a connection before entering the data transfer phase. After data transmission is completed, the connection termination closes the connection and releases all allocated resources.

A TCP connection is managed by an operating system through a resource that represents the local end-point for communications, the Internet socket. During the lifetime of a TCP connection, the local end-point undergoes a series of state changes:[16]

To establish a connection, TCP uses a three-way handshake. 

1. Before a client attempts to connect with a server, the server must first bind to and listen at a port to open it up for connections: this is called a passive open. 
2. Once the passive open is established, a client may initiate an active open. To establish a connection, the three-way (or 3-step) handshake occurs:

SYN: The active open is performed by the client sending a SYN to the server. The client sets the segment's sequence number to a random value A.

SYN-ACK: In response, the server replies with a SYN-ACK. The acknowledgment number is set to one more than the received sequence number i.e. A+1, and the sequence number that the server chooses for the packet is another random number, B.

ACK: Finally, the client sends an ACK back to the server. The sequence number is set to the received acknowledgement value i.e. A+1, and the acknowledgement number is set to one more than the received sequence number i.e. B+1.

At this point, both the client and server have received an acknowledgment of the connection. The steps 1, 2 establish the connection parameter (sequence number) for one direction and it is acknowledged. The steps 2, 3 establish the connection parameter (sequence number) for the other direction and it is acknowledged. With these, a full-duplex communication is established.

https://www.cloudflare.com/learning/ssl/transport-layer-security-tls/


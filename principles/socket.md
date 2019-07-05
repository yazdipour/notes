# Socket

* In Unix, every I/O action is done by writing or reading a file descriptor.
* A file descriptor is just an integer associated with an open file and it can be a network connection, a text file, a terminal, or something else.
* Most of the application-level protocols like FTP, SMTP, and POP3 make use of sockets.

## Socket Types

### Stream Sockets

* Delivery is guaranteed.
* Use TCP for data transmission.
* If you send through the stream socket three items "A, B, C", they will arrive in the same order − "A, B, C".
* If delivery is impossible, the sender receives an error indicator
* Data records do not have any boundaries.

### Datagram Sockets

* Delivery is NOT guaranteed.
* Use UDP for data transmission.
* They're connectionless because you don't need to have an open connection as in Stream Sockets − you build a packet with the destination information and send it out.

### Raw Sockets

* These provide users access to the underlying communication protocols, which support socket abstractions.
* These sockets are *normally datagram oriented*, though their exact characteristics are dependent on the interface provided by the protocol.
* Raw sockets are not intended for the general user; they have been provided mainly for those interested in developing new communication protocols, or for gaining access to some of the more cryptic facilities of an existing protocol.

### Sequenced Packet Sockets

* They are *similar to a stream socket*, with the exception that record boundaries are preserved.
* This interface is provided only as a part of the Network Systems (NS) socket abstraction.
* Sequenced-packet sockets allow the user to manipulate the Sequence Packet Protocol (SPP) or Internet Datagram Protocol (IDP) headers on a packet or a group of packets, either by writing a prototype header along with whatever data is to be sent, or by specifying a default header to be used with all outgoing data, and allows the user to receive the headers on incoming packets.

## Client Server Model (TCP)

![socket](https://www.tutorialspoint.com/unix_sockets/images/socket_client_server.gif)

* `listen()`    Invite Incoming Connections Requests API
* `bind()`      Set Local Address for Socket API
* `accept()`    Wait for Connection Request and Make Connection API
* `send()`      Send Data API
* `recv()`      Receive Data API
* `close()`     Close File or Socket Descriptor API
* `socket()`    Create Socket API
* `setsockopt()`Set Socket Options API
* `select()`    Wait for Events on Multiple Sockets API
* `gethostbyname()`  Get Host Information for Host Name API
* `connect()`   Establish Connection or Destination Address API

[src](https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_74/rzab6/connectionor.htm)

## OS Api

* Winsock: in Windows
* bsdsocket: in BSD & MACOS

## Reference

* [Unix Socket Tutorial](https://www.tutorialspoint.com/unix_sockets/what_is_socket.htm)
* [The WebSocket Protocol Document Page](https://tools.ietf.org/html/rfc6455#section-7.4)

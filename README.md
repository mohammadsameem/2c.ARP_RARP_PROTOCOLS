# 2c. SIMULATING ARP / RARP PROTOCOLS

## AIM
To write a Python program for simulating ARP and RARP protocols using TCP.

## ALGORITHM

### Client
1. Start the program.
2. Establish a socket connection between the client and the server.
3. Get the IP address (ARP) or MAC address (RARP) to be converted.
4. Send this address to the server.
5. Receive the corresponding MAC address (ARP) or IP address (RARP) from the server.

### Server
1. Start the program.
2. Accept the socket connection created by the client.
3. Maintain a table in which IP addresses and their corresponding MAC addresses are stored.
4. Read the address sent by the client.
5. Map it to the corresponding address in the table and return it to the client (or return "Not Found").

## PROGRAM - ARP

### Server
```python
import socket

table = {"192.168.1.10": "00:1A:2B:3C:4D:5E", "192.168.1.20": "00:1A:2B:3C:4D:5F"}

with socket.socket() as s:
    s.bind(("localhost", 9000))
    s.listen(1)
    c, _ = s.accept()
    with c:
        while ip := c.recv(1024).decode():
            c.send(table.get(ip, "Not Found").encode())
```

### Client
```python
import socket

with socket.socket() as s:
    s.connect(("localhost", 9000))
    while ip := input("Enter logical address: "):
        s.send(ip.encode())
        print("MAC address:", s.recv(1024).decode())
```

## OUTPUT - ARP
<img width="1892" height="235" alt="image" src="https://github.com/user-attachments/assets/cffa07ef-4f46-48db-9532-6a327b717e17" />


## PROGRAM - RARP

### Server
```python
import socket

table = {"00:1A:2B:3C:4D:5E": "192.168.1.10", "00:1A:2B:3C:4D:5F": "192.168.1.20"}

with socket.socket() as s:
    s.bind(("localhost", 6000))
    s.listen(1)
    c, _ = s.accept()
    with c:
        while mac := c.recv(1024).decode():
            c.send(table.get(mac, "Not Found").encode())
```

### Client
```python
import socket

with socket.socket() as s:
    s.connect(("localhost", 6000))
    while mac := input("Enter MAC address: "):
        s.send(mac.encode())
        print("Logical address:", s.recv(1024).decode())
```

## OUTPUT - RARP
<img width="1917" height="287" alt="image" src="https://github.com/user-attachments/assets/8fbd3f82-d792-442b-92b5-2a987d3497db" />


## RESULT
Thus, the Python program for simulating ARP and RARP protocols using TCP was successfully executed.

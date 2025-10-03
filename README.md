# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
## Server
```
import socket 

server = socket.socket() 
server.bind(('localhost', 8000)) 
server.listen(5) 
print("Server listening on port 8000...")

c, addr = server.accept()
print("Connection from:", addr)

size = int(input("Enter number of frames to send: "))
frames = list(range(size))
window_size = int(input("Enter window size: "))

st = 0
i = 0

while i < len(frames):
    st += window_size
    c.send(str(frames[i:st]).encode())
    ack = c.recv(1024).decode()
    if ack:
        print("Client:", ack)
        i += window_size
    else:
        print("No ACK received. Closing...")
        break

c.close()
server.close()

```
## Client
```
import socket 

s = socket.socket() 
s.connect(('localhost', 8000))

while True:
    data = s.recv(1024).decode()
    if not data:
        print("Server closed connection.")
        break

    print("Server sent frames:", data)
    s.send("Acknowledgement received from client".encode())

s.close()
```

## OUPUT

<img width="1469" height="476" alt="Screenshot 2025-09-29 155517" src="https://github.com/user-attachments/assets/2ac79fdf-4364-426b-9f1e-ec1be4edb2a9" />


## RESULT
Thus, python program to perform stop and wait protocol was successfully executed

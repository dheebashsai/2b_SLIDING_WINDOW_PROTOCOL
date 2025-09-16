<img width="1949" height="2032" alt="Screenshot 2025-09-16 092026" src="https://github.com/user-attachments/assets/d6d5836a-b745-4ab8-8181-859ee152acae" /># 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
 #client.py:
 ```
import socket

s = socket.socket()
s.connect(('localhost', 8000))

# Get number of frames and window size
size = int(input("Enter number of frames to send: "))
frames = list(range(size))

window_size = int(input("Enter Window Size: "))

i = 0
while i < len(frames):
    # Select frames for this window
    window = frames[i:i + window_size]

    # Send window of frames
    s.send(str(window).encode())
    print(f"Sent frames: {window}")

    # Wait for ACK
    ack = s.recv(1024).decode()
    if ack:
        print(ack, "\n")
        i += window_size  # Move window forward

s.close()

```
 #server.py:
 ```
import socket

# Create socket
s = socket.socket()
s.bind(('localhost', 8000))
s.listen(1)

print("Server is waiting for connection...")
c, addr = s.accept()
print("Connected with client:", addr)

while True:
    data = c.recv(1024).decode()
    if not data:
        break
    print("Received frames:", data)

    # Send ACK back
    c.send("ACK received from server".encode())

c.close()
s.close()

```
## OUPUT
<img width="1949" height="2032" alt="Screenshot 2025-09-16 092026" src="https://github.com/user-attachments/assets/cbe98ffd-43ab-46f6-a446-a937b426f972" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed

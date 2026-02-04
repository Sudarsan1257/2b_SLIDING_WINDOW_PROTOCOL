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
### SERVER.py
```
import socket
s = socket.socket()
s.bind(('localhost', 9999))
s.listen(1)
print("Server listening...")
conn, addr=s.accept()
print(f"Connected to {addr}")


while True:
    frames = conn.recv(1024).decode()
    if not frames:
        break


    print(f"Received frames: {frames}")
    ack_message = f"ACK for frames: {frames}"
    conn.send(ack_message.encode())
conn.close()
s.close()
```
### CLIENT.py
```
import socket

c = socket.socket()
c.connect(('localhost', 9999))

size = int(input("Enter number of frames to send: "))
I = list(range(size))

print("Total frames to send:", len(I))
s = int(input("Enter Window Size: "))

i = 0
while i < len(I):
    st = i + s
    frames_to_send = I[i:st]
    print(f"Sending frames: {frames_to_send}")
    
    c.send(str(frames_to_send).encode())

    ack = c.recv(1024).decode()
    if ack:
        print(f"Acknowledgment received: {ack}")
        i += s  

c.close()

```
## OUTPUT
<img width="805" height="119" alt="Screenshot 2026-02-04 140636" src="https://github.com/user-attachments/assets/5841a1c5-3a36-402d-91a8-c6e18ac27162" />
<img width="765" height="166" alt="Screenshot 2026-02-04 140629" src="https://github.com/user-attachments/assets/b5a74444-4c13-4cd4-802a-8239bfcb7177" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed

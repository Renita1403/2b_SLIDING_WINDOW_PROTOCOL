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

SERVER.PY:
import socket
sock = socket.socket()
sock.bind(('localhost',6000))
sock.listen(5)
c, addr = sock.accept()
size = int(input("Enter number of frames to send : "))
frames = list(range(size))
window = int(input("Enter Window Size : "))
i = 0
while i < len(frames):
    st = i + window
    c.send(str(frames[i:st]).encode())
    ack = c.recv(1024).decode()
    print(ack)
    i += window
c.close()
sock.close()

CLIENT.PY:
import socket
s = socket.socket()
s.connect(('localhost',6000))
while True:
   data = s.recv(1024).decode()
   if not data:
        break
   print(data)
   s.send("ACK received".encode())
s.close()

## OUPUT:

<img width="1857" height="942" alt="Screenshot 2026-05-20 191316" src="https://github.com/user-attachments/assets/956ac8b4-f701-46bb-bc1c-86c724c871de" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed

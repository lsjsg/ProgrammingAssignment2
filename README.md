# Programming Assignment 2
## Secure File transfer
- **This program only support Oracle JDK 8 runtime, not able to run on JDK 11 environment**  
- **OpenJDK got some problem with the buffer and have chance to failed to finish the verification**   
This program allows us to transfer files from client to server safely. Which proceeds from verify server to verify client, then transfer the files using RSA or AES encryption method.
### To run the program
#### Server
The server will start and keep running and listening to the client connection request.  
The server code allows multiple clients to connect at the same time.  
If the connection is successful, then the server will create a new thread for the client to transfer the files (the server side will create some more thread to decrypt and write the files to disk even though the files have finished transfer, these threads may keep on running even though the connection is closed, but once after they have finished running, they will close automatically)  

~~~shell
# For CP 1 with default parameter port 12345
javac ServerCP1.java && java ServerCP1 
# For CP 1 you can specify the port to use port = arg[0]
javac ServerCP1.java && java ServerCP1 1234
# For CP 2 with default parameter port 123
javac ServerCP2.java && java ServerCP2
# For CP 2 you can specify the port to use port = arg[0]
javac ServerCP2.java && java ServerCP2 1234
~~~
#### Client
The client code will automatically verify the server and transfer the files in sequence.  
Multiple instances can work parallelly connect to the same server.  
- **The client code may finish first before the server code finish, server code needs some more time to decrypt and write to file**   
~~~shell
# For CP 1 with default parameter default port: 12345 default server: localhost default file: 100.txt
javac ServerCP1.java && java ServerCP1
# For CP 1 port = args[0] server = args[1] files = args[2 - n]
javac ServerCP1.java && java ServerCP1 12345 localhost 100.txt 10000.txt 100000.txt
# For CP 2 with default parameter default port: 123 default server: localhost default file: 100.txt
javac ServerCP2.java && java ServerCP2
# For CP 2 port = args[0] server = args[1] files = args[2 - n]
javac ServerCP2.java && java ServerCP2 123 localhost 100.txt 10000.txt 100000.txt
~~~
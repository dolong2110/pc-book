# pc-book




- RPC stands for **R**emote **P**rocedure **C**alls
It is a protocol allows a program to
  - execute a procedure of another program located in other computer.
  - without developer explicitly coding details for remote interaction


### 2. Stubs 
- gRPC needs stubs to communicate between services
- Generate stubs:
  - first need API contract: contains services and payload messages in protocol buffered file
  - Why gRPC uses protocol buffer:
    - human-readable interface definition language (IDL)
    - automatically code generators for many languages
    - represent data in binary format:
      - smaller size
      - faster to transport
      - more efficient to serialize and deserialize than some text-based format like JSON or XML
    - strong typed-API contract between client and server which is super safe
    - conventions for API evolution
      - ensure backward and forward compatibility

### 3. HTTP/2
- gRPC uses HTTP/2 as its transfer protocol
- Great features gRPC inherits from HTTP/2:
  - binary framing:
    - more performance and robust
    - lighter to transport, safer to decode compare to other text-based protocol
    - great combination with protocol buffer
  - Header compression using HPACK:
    - reduce overhead and improve performance
  - multiplexing:
    - client and server can send multi requests and responses in parallel over a single TCP connection.
    - reduce latency and improve network utilization
  - allow server push:
    - one request from client, server can send back multi response -> valuable to reduce the round trip latency between client and server when server knows exactly what resources the client will be needed and send them before they are even requested

### 4. How HTTP/2 vs HTTP/1.1

| | HTTP/2 | HTTP/1 |
|---| --- | ---|
| Transfer Protocol | Binary | Text |
| Headers | Compressed | Plain text |
| Multiplexing | Yes | No |
| Requests per connections | multiple | 1 |
| Server push | Yes | No |
